---
description: Crowd-sourcing annotation tasks on online platforms.
---

# Crowd-sourcing annotation tasks

To annotate a small amount of data, one can just do it on their computer. For this, the default interface is supposed to be a perfect match. At the other end of the spectrum, some annotation tasks are just too huge, and need to be crowd-sourced. [Amazon Mechanical Turk](https://www.mturk.com/) \(mturk\) is the perfect service for that. It comes in two sides. A "**requester**" is defining a set of tasks while a "**worker**" is performing the tasks. Workers are payed by requesters through mturk service.

Mturk is based on the concept of a "**HIT**" \(Human Intelligence Task\) as the task unit. The simplest way of quantification in our case is **one image &lt;=&gt; one HIT**. In the following, I will describe first how to set up accounts on mturk, then how to use this annotation application for the HITs.

## Registering for sandbox accounts

Defining "real" tasks on mturk is obviously going to cost you money. But fortunately, mturk also have testing equivalent of the normal requester and worker environments, called **sandbox** environments. So the first thing to do is to registering for a [requester sandbox](https://requestersandbox.mturk.com/) and a [worker sandbox](https://workersandbox.mturk.com/) account.

## Creating a project template

As a requester, create a new project by going to the "Create" tab and clicking on "New Project".

![](.gitbook/assets/mturk-requester-create.jpg)

Go to the "Other" category and click and "Create Project &gt;&gt;".

![](.gitbook/assets/mturk-requester-other.png)

In the tab "\(1\) Enter Properties", fill the fields as you wish but you need to set a "Reward per assignment", and at the question "Require that Workers be Masters to do your HITs", answer "No" to be able to test your own HITs. Once filled, click on the bottom button "Design Layout" to validate and go to the next tab. You will get a page looking like this one.

![](.gitbook/assets/mturk-requester-design.png)

Now click on the "Source" button to edit the source code, and replace the code by the following one. The structure of this chunk of code is explained in the next section.

{% code-tabs %}
{% code-tabs-item title="mturk-template.html" %}
```markup
<div>
	<input type="hidden" value="" name="annotation-data" id="annotation-data"/>
	<style>html, body, .style-elements { height: 100% } #mturk_form { display: none }</style>
	<script src="https://annotation-app.pizenberg.fr/elm-pep.js"></script>
	<script src="https://annotation-app.pizenberg.fr/Main.js"></script>
	<script charset="utf-8">
		// Function returning the size of the container element for the app.
		// In our case, the full layout viewport.
		const layoutViewportSize = () => ({
			width: document.documentElement.clientWidth,
			height: document.documentElement.clientHeight
		});
		const containerSize = layoutViewportSize;

		// The image to display
		const img = {
			width: ${img_width},
			height: ${img_height},
			url: "${img_url}"
			// comment to prevent mturk templating system to merge those two '}'
		};

		// Set elm app flags
		const flags = {
			deviceSize: containerSize(),
			mturkMode: true,
			images: [img],
			config: `{
				"classes": [],
				"annotations": [ "point", "bbox", "stroke", "outline", "polygon" ]
			}`
		};

		// Start elm app.
		const app = Elm.Main.fullscreen(flags);
	</script>
	<script src="https://annotation-app.pizenberg.fr/ports-mturk.js"></script>
</div>

```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now your editing area should look like the following.

![](.gitbook/assets/mturk-requester-source.png)

If the "Source" button is not pressed, it means that mturk had a bug. It happens sometimes, due to sign out or other mysterious mturk events. If you are like this, with the "Source" button pressed and the code pasted in, we can continue. Click again on the "Source" button to leave the source mode. Now you should have something looking like the following, which is totally normal.

![](.gitbook/assets/mturk-requester-source-out.png)

Now click on the bottom "Preview" button. It moves you to the third tab, a notification like "Your project was successfully saved." and a preview of what your HIT would look like. The preview should be empty. Again, **this is normal, don't panic** ;\). In case you open your JavaScript browser console, you will even see a runtime error, of the kind "SyntaxError: missing } after ...". This error is due to mturk templating system. You will understand the reason for this in the next section. Now simply click on the bottom "Finish" button and you are done with the project template. You should be back to the "Create" tab with a new project entry looking like the following.

![](.gitbook/assets/mturk-requester-project-created.png)



