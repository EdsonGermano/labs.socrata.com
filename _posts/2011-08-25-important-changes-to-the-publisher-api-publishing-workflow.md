--- 
title: "Important Changes to the Publisher API: Publishing Workflow"
layout: post
---

__Update:__ The rollout of the Publishing Workflow has completed. If you encounter any problems with the new workflow, or if you need help migrating your processes or code, please [open a support ticket](http://support.socrata.com/tickets/new) and we'll be glad to help you.

__Update:__ The Publishing Workflow rollout has been delayed until 9/20. As before, we'll provide updates here when the actual deployment has been completed.

__Update:__ The Socrata team will be rolling out the publisher API changes on the evening (Pacific Daylight Time) of Thursday, September 15th. We'll post another notification when the deployment is complete.

_The following is an important announcement for users of the Socrata Open Data Publisher API. If you don't use the Publisher API to update datasets, it doesn't pertain to you. But if you're interested, feel free to read on, because we think it's pretty cool._

The Socrata team is excited to announce an important update to the Publisher API: The Socrata Publishing Workflow.

Details of the [Publishing Workflow](/publisher/workflow) have been available for several months, and now that many of our customers have migrated their systems to be prepared for the change, we're making the final preparations to launch it to our shared production platform.

The Publishing Workflow does change the way that publishers must interact with our platform, so this is an important change to be aware of and prepared for. We plan on rolling out the change during the week of September 12th. Final deployment timing and details will be shared with all publishers before the change is deployed.

For more details, see the documentation on the [Publishing Workflow](/publisher/workflow) or read on.

~

## What is it?

The Publishing Workflow changes some of the fundamental ways in which datasets work on Socrata. Instead of being a dataset being an always-live representation of your data - where consumers see changes or updates you make in real time - datasets will have two states: `Published` and `Working Copy`

A `Published` dataset is a static, finalized copy of your data intended for sharing either with the public or within your organization. It represents a particular version of your dataset, and thus is locked against editing. In order to make edits to your datasets, you must first create a `Working Copy`.

A `Working Copy` is an editable version of your dataset that is distinct from the `Published` copy. Think of it as an internal draft copy of your dataset that you can collaborate with your coworkers on. You can make whatever changes you want to the `Working Copy` without those changes being reflected in the Published copy. When you're done with making your changes, you can "publish" the `Working Copy` to be the new `Published Copy`, and your changes will become live. Even better, the old `Published Copy` becomes a `Snapshot`, which you can reference as a historical version of the dataset.

## What are the benefits of it?

There are many benefits to the Publishing Workflow, but here are a few of our favorites:

- Since there is an explicit publishing step, `Published` copies can be heavily cached, allowing us to improve the performance of datasets both large and small
- Since you can make changes to a `Working Copy` without affecting the `Published` copy, you have a chance to review updates for correctness, clarity, and completeness before they go live. You can even share them within your organization to get approval before the changes are published. No longer will you have to fear that the changes or updates you're making will break your dataset!
- Since old versions of your dataset are archived as `Snapshots`, and even accessible via the Consumer API, you can keep historical archives of your dataset around to show how it has changed over time.

## How does it impact me? How do I prepare for the change?

The Publishing Workflow will be available both in the online Socrata Publisher tools and also in the Publisher API. For users of the online Publisher tools, all you'll need to do is click the provided button to create a `Working Copy` before modifying your dataset.

For users of the Publisher API, there are a few small modifications you'll need to make to your client. Since you'll need to create a `Working Copy` of your dataset, and then publish your changes after you're done, there are two additional calls you'll need to make to the `/publication` API in your workflow, like wrapping database updates in a transaction:

1. First you'll need to call `POST /api/views/$view_id/publication.json?method=copy` to create the `Working Copy`. The response to this service call will include the metadata and ID of the `Working Copy` that was created.
2. Next you'll make your updates to your dataset as usual, this time substituting the `Working Copy` for the original dataset.
3. Finally you'll call `POST /api/views/$working_copy_view_id/publication.json` in order to publish the `Working Copy` as the new `Published Copy`

That's it. For more details, see the detailed documentation on the [Publishing Workflow](/publisher/workflow).

## tl;dr - That was all far too much, give me the short version

Socrata will soon be deploying changes to the Publisher API that will make it possible for you to isolate changes to datasets from the version consumers on your data site will see.

You'll need to update your Publisher API client by the week of September 12th to take advantage of these changes. For more details, see the documentation on the [Publishing Workflow](/publisher/workflow).

## Help! I'm not sure how to migrate my code!

If you have additional questions about the Publishing Workflow that aren't answered by here or in the [documentation](/publisher/workflow), please email your questions or concerns to [support@socrata.com](mailto:support@socrata.com).