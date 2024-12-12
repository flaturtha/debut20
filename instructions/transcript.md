0:00
Hi, I'm Liam,
0:01
and I'm a Theme Developer Evangelist here at Shopify.
0:04
In this video, we'll be looking at how to work with JSON templates for themes.
0:08
JSON templates allow merchants to add and reposition dynamic content
0:13
on all pages.
0:14
And this unlocks a new range of customization options
0:17
for merchants on their storefronts.
0:19
The inclusion of JSON templates is also a requirement
0:23
for submitting a theme to the Shopify theme store.
0:26
So, if you're looking to launch a theme on our marketplace,
0:28
you'll need to implement JSON templates on pages.
0:31
Let's dive in to learn more.
0:33
So, to start off, let's take a look at one of our themes,
0:36
which already has JSON templates applied to it to see how this will look
0:42
and behave for a merchant when they are customizing their theme.
0:46
So, I'm inside my development store and I have our Dawn theme,
0:50
one of our flagship free themes installed,
0:53
which already has JSON templates set up and is also available on GitHub.
0:59
If you want to see a reference for how JSON templates can be set up.
1:05
So, if we go into the theme editor
1:07
and we navigate to any page which is not the home page
1:11
we can see, we have a new add section option that is available
1:17
in the theme editor.
1:18
When we click on this,
1:19
we're able to access a range of different sections
1:24
which are available for this page type.
1:28
We'll also look at how these can be enabled later,
1:32
and this is the same then for any other page on this storefront.
1:36
We will have an add section option which is appearing here,
1:40
and this is actually enabled by using JSON templates.
1:45
So, if we navigate to the actual code editor within the Shopify admin
1:50
and we take a look at the templates directory of the theme,
1:54
we can see here that all of the templates are using .JSON files
2:02
as opposed to .LIQUID files,
2:05
which are used previously in our vintage themes.
2:10
So, you can see as an example and we have a page .JSON,
2:15
and this is for regular static pages to apply this template to it.
2:21
And inside this JSON file,
2:23
we can see an array here where we are indicating that there are sections
2:28
assigned to this template. We have a section called Main.
2:33
We have a field with type, and the type value is main page.
2:40
So what this means is that
2:42
this page template has one main page section,
2:49
and this main page section or this main page type
2:54
corresponds with a section that's inside our sections directory here.
3:00
So, if we navigate here, we should see our main page .LIQUID,
3:06
and this actually contains all of the markup and liquid that's needed
3:10
for the page to render. So we have our page .title.
3:14
We have our page .content contained within different containers or headers,
3:20
depending on what that object is.
3:24
So, if we look back at our page .JSON templates we see here,
3:31
essentially the template is telling the page to render this main page section.
3:36
And we also have an order section area here
3:41
where we can define in which order, if there is multiple sections,
3:45
in which order the sections will be appearing.
3:48
And so what's very interesting as well, if we go back to our
3:57
theme editor
4:00
and we go to that page. So this is the page that's rendering using
4:06
the page .JSON and you can see we can add a section.
4:11
So, if we just added
4:14
a contact form section, for example, and we save this.
4:21
Now, when we return back to the code editor.
4:28
And we look at our main page, Liquid.
4:32
But if you look at our page .JSON.
4:35
We can see here that this is actually just changed.
4:40
So you saw that I added a contact form section to the page
4:47
and what has happened on the backend in the page .JSON is,
4:50
this is updated to include that section.
4:53
So we have this code, which corresponds to that new section that we created,
5:00
tells me what the type is.
5:01
It's a contact form section
5:04
and we can even see that within our sections directory,
5:08
if we look at contact form.
5:11
So it's including this section into the template
5:14
and you can see as well our order has also updated,
5:18
So, you can see from this using JSON templates,
5:22
it creates a much stronger connection between the theme editor
5:27
and the theme files itself.
5:30
So, now that we understand the basics of working with JSON templates,
5:33
let's take a look at how we can migrate
5:35
a theme which uses liquid templates to using JSON templates
5:40
so that sections are available on all pages.
5:42
In my case, I have a theme called Liam's Theme here,
5:47
which is using all liquid templates for rendering different pages.
5:54
And as you can imagine, if I tried to customize the theme and I go to
6:00
a non home page page, I'm not seeing that add section option appearing here.
6:08
So, this is something I want to change.
6:10
So essentially, what we will need to do
6:12
is migrate any content from our .liquid templates
6:16
into existing sections
6:18
or create new sections to migrate that content into.
6:22
Then, we will need to delete the .liquid templates
6:26
and replace them with .JSON templates for each file type.
6:31
The very first thing that we should do is to create a copy of our theme
6:37
or a backup so that we have something to revert back to
6:40
if we need to undo any changes.
6:42
And just to mitigate any risk around making any destructive changes
6:47
to our theme.
6:49
I'm using the Shopify CLI to edit my theme locally
6:54
on my local computer,
6:56
where I can test my changes before pushing it back up to the live store
7:01
in an unpublished theme state.
7:04
And if you'd like to see how you can set up
7:06
that local development environment for your theme,
7:09
we have a very good video that we recently published,
7:13
that you can check out that will link in the description below.
7:17
So, the first template that we're going to migrate over
7:19
from being a .liquid template to being a .JSON template
7:23
is our product .liquid file.
7:28
So within this file, we can see we're including some sections.
7:33
And there's also some code below the sections.
7:37
But the first thing I'm going to look at is that this section includes tags
7:41
and we can see here there's a section called product-template
7:45
being included.
7:46
So I'm going to find that section in our section directory here,
7:53
product-template.
7:55
And we can see in this section,
7:58
it actually contains all of the markup that's really required
8:02
for our product page. So things like product media,
8:06
we will have a product form
8:09
as well that will include everything like our add to cart buttons.
8:15
So this is telling me this is really the main section for the product page.
8:22
So what we're going to do is we're going to relocate
8:25
the content that appears in this template into our product template section.
8:32
And also we'll also take a note of our product recommendations
8:38
section being included here, too,
8:41
and we'll be adding this into the JSON template.
8:43
So, I'm simply going to take the code that is appearing below
8:49
where the sections are being included,
8:51
and I'm going to cut and paste those into our product template section.
8:58
I'm going to add it just above where the opening schema tags appear.
9:04
So it's at the bottom of the template because in our template file,
9:10
originally they were appearing below where the section was being included.
9:14
So, by adding it below all of the other markup,
9:18
I can ensure that it will remain in the same location when
9:23
our content is migrated over.
9:26
So, once I save that, what I'm also going to do,
9:30
which is not required but will make it easier to manage
9:35
the different sections in your theme,
9:37
is I'm going to rename the
9:41
the section that I've migrated my content into from product template
9:45
to main product.
9:51
So, the reason I am doing this is it will just make it
9:54
a lot clearer in my sections directory, which sections are required as the,
10:01
you know, the basic or the main sections that contain things like, in this case,
10:07
product form.
10:08
But if it was pages, it could be the page title and page content.
10:14
So, once I have that renamed, I can return back to the product.liquid.
10:20
Take a note again of where product recommendations is appearing.
10:25
And now, what I will actually need to do is I will need to delete
10:29
the product.liquid file.
10:33
The reason why I need to delete this is
10:35
because you can't have both a product.JSON
10:40
and a product.liquid files existing within the templates folder.
10:46
So, we will remove or delete our product.liquid
10:52
from our Templates folder, then create a new file called product.json
10:59
in our Templates directory.
11:01
And what we're going to do is we're going to populate that with some JSON
11:06
that is going to assign our specific section
11:12
to the product template.
11:14
So, this snippet can actually be found in a documentation
11:20
that I will link in the description below on migrating to JSON templates.
11:26
So, you can take exactly this snippet.
11:28
But essentially what we're doing here is we're using JSON to create some arrays
11:34
and objects where we assign which section is appearing on this template,
11:40
and we're going to use the section that we created, which was main-product.
11:47
And essentially, what this is doing is it's saying this template
11:51
or this page type uses the main products section as its main section.
11:57
So, once we save this, we should be able to migrate to our development instance
12:04
of the online store editor.
12:07
And when we navigate to a product page, we'll now be able to add sections.
12:13
So, all of our sections that are accessible to this page
12:16
will be appearing here.
12:19
So, this is great. We've been able to take our .liquid product page
12:25
and we've been able to migrate it to using JSON templates.
12:28
So, now sections are appearing here, which is brilliant.
12:31
So, we have sections appearing on our product page,
12:34
but you will probably remember that there was also
12:37
a recommendation section appearing on our page.
12:41
So, the next step is actually going to be adding that back in.
12:46
So, we already have that section appearing here.
12:49
It's called product-recommendations.liquid.
12:53
So we're really just going to need to reassign that to our
12:59
template.
13:00
So, to do that, I'm going to assign a new section.
13:05
I'm going to call it recommendations.
13:12
I'm going to also
13:17
add the type field.
13:20
And the type field needs to correspond exactly with the name of the
13:27
section that we're including.
13:29
So, in our case, the type will be product-recommendations.
13:39
And, of course, I'm going to also need to adjust the order.
13:44
So, I will add in...
13:48
So, you'll notice, as well, I'm using recommendations as the order
13:51
because this is the name that I've assigned it within the JSON template.
14:01
So, now, once I've saved that,
14:04
I can go back to our development team instance where
14:09
we are, you know, having our server running.
14:15
And, if I reload this,
14:21
I now see, on this side panel, I have my product recommendations.
14:25
And you can see the recommendations are now appearing here, as well.
14:30
So, this is really great
14:31
And, if I wanted to, I could even move that around to.
14:36
So, this is great. I've now recreated exactly my product template
14:41
as it existed on the... As a .liquid template.
14:47
But now I'm able to add sections.
14:49
So, essentially the same technique can be used
14:53
for all of the other types of pages
14:58
to allow you, then, to be able to add sections on all of these pages.
15:03
So, while the basic method will remain the same,
15:06
where you relocate content into sections
15:10
and, then, create a new JSON templates,
15:14
there are some instances where this might be a little bit more complex
15:17
or a little bit nuanced, than others.
15:20
So, for example, I have a article template
15:25
where I am including a section for the main article template
15:32
section file.
15:34
But you can see here we have some content that's appearing both, above and below.
15:41
In this case,
15:42
this is content that's related to comments on our storefront.
15:50
So, one method for dealing with this is to actually create
15:54
a new section where we will contain all of the content that,
16:00
in this case, is related to comments.
16:03
So, the very first thing I will do is I will create a new section.
16:10
I'll call it blog-comments
16:15
.liquid
16:19
And then, what I'll do is I will move
16:21
all of the content related to comments into this file.
16:32
So, we can delete this from the article.liquid template
16:38
and all we're going to keep, for the moment, is the content
16:43
and markup that's related specifically to the article.
16:49
So, again, I'll take all of the code related to comments.
16:56
and add it into my new section file.
17:01
So, I now have that saved.
17:03
It's not being included anywhere,
17:05
and here I just have, in my liquid template,
17:09
I just have the component for article
17:14
where I'm also including the article template section.
17:19
So, my next stop is going to be finding this section.
17:24
So, you see here article-template.liquid
17:28
So, all of this code is being included in this line.
17:35
So, what I'm going to do is, above the section tag,
17:40
I'm going to take that code and I'm going to add it
17:45
above the...
17:50
Above the existing code.
17:54
Just going to indent it, so that it's appearing correctly.
17:58
So, these are all of the opening
18:01
elements and containers.
18:04
I also have
18:07
those closing tags, too, which would appear here.
18:13
So, this will correspond with the opening article tag, here.
18:19
And, essentially, that's just repositioning
18:21
the tags that are reappearing above and below this section tag,
18:30
which represents everything that was in this existing article-template.liquid
18:38
Again, what I'll do is I will rename this file
18:43
to main-article.liquid
18:47
Again, just to make it a little bit easier for me to organize
18:50
and to quickly understand which of my sections are main sections
18:56
for specific templates.
19:01
And then, in the templates folder, again, I'm going to delete this file.
19:13
And I am going to, then, add...
19:18
In the templates directory, I'm going to add a new
19:23
article.json.
19:27
So, once I've created my new JSON template for the article,
19:32
I'm going to, again, use a very similar process as before,
19:39
where I had some JSON here, where I'm assigning name, sections, main, type;
19:44
different attributes and fields, here.
19:48
So, I'm giving it a name of article.
19:50
I'm also having including sections.
19:54
So, the main that I just added was main-article.
20:04
And the orders, for the moment's just going to be main.
20:07
So, I'm going to just save that, for the moment,
20:11
and then navigate back to my
20:14
development theme instance, where I have the online...
20:18
I have to store editor open.
20:20
So, when I navigate to the blog article,
20:25
I can see the content is appearing correctly
20:27
and I have the option to add sections,
20:30
which is telling me that the JSON template has been applied correctly.
20:34
But we are missing our comments here.
20:37
So, what I'm going to do is I'm going to navigate back to the code editor
20:43
and, again, I'm going to assign a new section to appear.
20:50
I'll call this comments.
20:56
And also, again, I have to
20:59
use the type field attribute to assign
21:05
the actual name of the section.
21:09
And if you can remember, we called it blog-comments.
21:18
And, again, we will need to adjust the order by using the...
21:26
The name that we've applied here, in the JSON template,
21:31
which is just comments.
21:34
So, now, once I've saved that,
21:36
I can return to our instance of the online store editor
21:43
and, when I refresh...
21:46
Yeah, here I'm seeing the comments component appearing
21:50
and it's appearing here, above the add section option, here.
21:58
So, this is great.
21:59
I was able to do a something a bit more complex
22:04
where we are splitting up our content that previously was in a liquid template
22:11
into different sections,
22:14
so that we can recreate exactly how our pages were appearing.
22:18
So now, we've looked at how JSON templates are structured,
22:22
how they can unlock sections on all pages of a store,
22:25
and how you can migrate an existing Shopify theme
22:28
from using liquid templates to using JSON templates.
22:32
To learn more about JSON templates,
22:34
you can check out the documentation links in the description below,
22:38
and you can also check out the Dawn theme on GitHub
22:41
to see an example of a theme that's using JSON templates across all page types.
22:46
For more information on Shopify Team Development,
22:49
make sure to subscribe to this channel and review the documentation
22:53
on shopify.dev
22:54
You can also join the Shopify Discord server
22:57
and meet fellow developers and ask questions.
23:00
Thanks so much for tuning in, and we'll be back with more soon.

