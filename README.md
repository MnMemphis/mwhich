MWhich -- Because searching Netflix, Amazon, Hulu, and iTunes sucks rocks
==========

## DESCRIPTION

MWhich was created because I'm lazy, and that laziness led to a loss of money.
Many times I end up watching on movie on iTunes simply because it is the first
place I look, even though had I taken another minute I would have found the
same movie available via Netflix Instant Play, or cheaper on Amazon's Video on
Demand service.

## API Access

Of course there is no easy standard for accessing this movie data, Tim
Berners-Lee's wishes be damned. Here is how these services are accessed:

  * Netflix: OData(!) via (http://odata.netflix.com)
  * Amazon: [Product Advertising(?) API](http://docs.amazonwebservices.com/AWSECommerceService/latest/DG/)
  * Hulu: Some hack of their publisher tool endpoint
  * iTunes: Their Store Web Service Search API via (http://www.apple.com/itunesaffiliates/API/AffiliatesSearch2.1.pdf)

## Usage

This is very bare bones right now:

To create a basic MWhich instance:

`m = MWhich::Client.new`

Search for a movie:

`m.search("The Prestige")`

At this time, this merely returns a hash of key/value pairs indicating which
services the movie or TV show was found on. The value is a simple string with
the type of media found and the title. Comments specific to each service
may also appear. For example:

  * If available on Netflix Instant Play, "Watch now!" will show up.
  * Hulu sometimes links to external content, "Not on hulu!" will identify this.
  * iTunes prices will be displayed

An array of services can be passed to the MWhich instance to limit the search.

Only want to search Netflix and Hulu?

    m = MWhich::Client.new(:services => [:netflix, :hulu])
    m.search("Knight Rider")

This is obviously imperfect, but does provide an initial abstracted search.