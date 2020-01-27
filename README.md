# Wikipedia API docs

Wikipedia API examples. For advanced use see [Official Mediawiki API documentation](https://www.mediawiki.org/wiki/API:Main_page)

Quick intro: 

- All client requests should contain `&origin=*` because of CORS. 
- Search term should be capitalize (`Tori Amos` not `tori amos`) if multiple words.
- You could request any wiki language you like

## Get an article

To GET full article for the requested title (`titles=belgrade`), with images and URL (`inprop=url`). Also, follows redirection (`redirects`) if necessary:

[https://en.wikipedia.org/w/api.php?action=query&titles=belgrade&prop=extracts|pageimages|info&pithumbsize=400&inprop=url&redirects=&format=json&origin=*](https://en.wikipedia.org/w/api.php?action=query&titles=belgrade&prop=extracts|pageimages|info&pithumbsize=400&inprop=url&redirects=&format=json&origin=*)

Previous request with minimal params:

https://en.wikipedia.org/w/api.php?action=query&titles=belgrade&prop=extracts&format=json

To get all images from the article:

https://en.wikipedia.org/w/api.php?action=query&titles=belgrade&prop=images&format=json

## Search articles

To GET first 10 search results with page title, extract and thumbnail image (`prop=extracts|pageimages`). Article extract is HTML by default:

https://en.wikipedia.org/w/api.php?action=query&generator=search&gsrsearch=belgrade&exintro=&prop=extracts|pageimages&format=json

To GET first 20 search results (`srlimit`) with page title and info (`prop=info`):

https://en.wikipedia.org/w/api.php?action=query&list=search&prop=info&inprop=url&utf8=&format=json&srlimit=20&srsearch=belgrade

To GET first 20 search results (`gsrlimit`) with page title, extract and thumbnail image (`prop=extracts|pageimages`). Article extract is set to plain text (`explaintext`):

https://en.wikipedia.org/w/api.php?action=query&generator=search&gsrlimit=20&prop=pageimages|extracts&exintro&explaintext&exlimit=max&format=json&gsrsearch=belgrade

To GET 10 search results with info and page URL:

https://en.wikipedia.org/w/api.php?action=opensearch&format=json&redirects=return&search=belgrade

### Advanced search params

- `gsrsearch=intitle:belgrade` (word "belgrade" is in title)
- `gsrsearch=prefix:belgrade` (article's title starts with the word "belgrade")

## Search images

To GET first 20 image files (`gsrnamespace=6`) from Wikimedia Commons with the term "Belgrade" in the filename (`gsrsearch=intitle:Belgrade`). Requested thumbnail size is 250px (`pithumbsize=250`):

https://commons.wikimedia.org/w/api.php?prop=pageimages|imageinfo|info|redirects&gsrnamespace=6&pilimit=max&pithumbsize=250&iiprop=extmetadata&iiextmetadatafilter=ImageDescription&action=query&inprop=url&redirects=&format=json&generator=search&gsrsearch=intitle:Belgrade&gsrlimit=20

Previous request without some params:

https://commons.wikimedia.org/w/api.php?prop=pageimages|info|redirects&gsrnamespace=6&pithumbsize=250&action=query&inprop=url&redirects=&format=json&generator=search&gsrsearch=intitle:Belgrade&gsrlimit=20

## GET main image

To get source of the main image of the article:

https://en.wikipedia.org/w/api.php?action=query&titles=Belgrade&prop=pageimages&format=json&pithumbsize=250

If you have problems, append `&origin=*` at the end of the route.

## GET quotes

To GET wiki quotes for requested term (`titles=Zen`). The API is the same, just the domain is different (`wikiquote.org`):

https://en.wikiquote.org/w/api.php?action=query&titles=Zen&prop=extracts|info&inprop=url&redirects=&format=json
