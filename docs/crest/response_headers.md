# Response Headers
## Cache-Control Header

In the XML API, the cached for time is reported in the XML body of the HTTP Response.  For Crest the cached for time (in seconds) is returned in a response header.

Header: Cache-Control
HeaderElement: max-age

The following is a Java code snippet that obtains the desired cached for time.  Where CacheControlHeader == "Cache-Control" and CacheControlMaxAge == "max-age"

    Header[] headers = response.getHeaders(CacheControlHeader);
    boolean found = false;
    AtomicInteger cacheTime = new AtomicInteger();
    if(headers != null && headers.length > 0)
    {
        for(int i=0; i < headers.length; i++)
        {
            HeaderElement[] headerElements = headers[i].getElements();
            for(int j=0; j < headerElements.length; j++)
            {
                if(headerElements[i].getName().equals(CacheControlMaxAge))
                {
                    cacheTime.set(Integer.parseInt(headerElements[i].getValue()));
                    found = true;
                    break;
                }
            }
        }
   }
