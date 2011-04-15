## Requirements

The truncator requires [Nokogiri][4] to parse out the HTML string.

## Usage

If you're using Jekyll, add the html_filters.rb file to your _plugins directory - this will give you the helper `truncatehtml` as a [Liquid][3] filter. In your views, you can use this function in the same way as you would use the normal `truncate` filter:

    page.content | truncatehtml: 500

## How it works

Given a snippet of HTML, we use Nokogiri to parse it into a tree. THis takes care of all of the messiness of dealing with HTML, and gives us back a tree of nodes representing the parsed snippet.

Now that we have the tree of nodes, we can traverse it depth-first. All text nodes are leaf nodes, so when we encounter one, we can count the length of the text.

Once we have all of the text we need, we continue traversing, but instead of counting text lengths, we delete all of the nodes we see after we've reached our maximum length.

After that, we have a tree of nodes that represent the truncated tree, and the can output the appropriate HTML.

[1]:https://github.com/MattHall/truncatehtml
[2]:http://pygments.org/
[3]:http://liquidmarkup.org
[4]:http://nokogiri.org/
