# 6.2.4 HTTP 통신 코드

* HTTP 주요 응답 코드 
<table>
  <thead>
    <tr>
      <th style="text-align:left">응답대역</th>
      <th style="text-align:left">응답코드</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Informational</td>
      <td>
        100
      </td>
      <td>
      continue
      </td>
    </tr>
    <tr>
      <td>
        101
      </td>
      <td>
      Switching protocols
      </td>
    </tr>
    <tr>
    <tr>
      <td rowspan="5">Success</td>
      <td>
        200
      </td>
      <td>
      OK
      </td>
    </tr>
    <tr>
      <td>
        201
      </td>
      <td>
      Created
      </td>
    </tr>
    <tr>
      <td>
        202
      </td>
      <td>
      Accepted
      </td>
    </tr>
    <tr>
      <td>
        203
      </td>
      <td>
      Non-authoritative information
      </td>
    </tr>
    <tr>
      <td>
        204
      </td>
      <td>
      No content
      </td>
    </tr>
    <tr>
    <tr>
      <td rowspan="3">Redirection</td>
      <td>
        301
      </td>
      <td>
      Moved permanently
      </td>
    </tr>
    <tr>
      <td>
        302
      </td>
      <td>
      Not temporarily
      </td>
    </tr>
    <tr>
      <td>
        303
      </td>
      <td>
      Not modified
      </td>
    </tr>
    <tr>
      <td rowspan="11">Client error</td>
      <td>
        400
      </td>
      <td>
      Bad Request
      </td>
    </tr>
    <tr>
      <td>
        401
      </td>
      <td>
      Unauthorized 
      </td>
    </tr>
    <tr>
      <td>
        402
      </td>
      <td>
      Payment required
      </td>
    </tr>
    <tr>
      <td>
        403
      </td>
      <td>
      Forbidden 
      </td>
    </tr>
    <tr>
      <td>
        404
      </td>
      <td>
      Not found 
      </td>
    </tr>
    <tr>
      <td>
        405
      </td>
      <td>
      Method not allowed
      </td>
    </tr>
    <tr>
      <td>
        407
      </td>
      <td>
      Proxy authentication required 
      </td>
    </tr>
    <tr>
      <td>
        408
      </td>
      <td>
      Request timeout
      </td>
    </tr>
    <tr>
      <td>
        410
      </td>
      <td>
      Gone  
      </td>
    </tr>
    <tr>
      <td>
        412
      </td>
      <td>
      Precondition failed
      </td>
    </tr>
    <tr>
      <td>
        414
      </td>
      <td>
      Request-URI too long
      </td>
    </tr>
    <tr>
      <td rowspan="5">Server error</td>
      <td>
        500
      </td>
      <td>
       Internal server error 
      </td>
    </tr>
    <tr>
      <td>
        501
      </td>
      <td>
      Not implemented
      </td>
    </tr>
    <tr>
      <td>
        503
      </td>
      <td>
      Service unnailable
      </td>
    </tr>
    <tr>
      <td>
        504
      </td>
      <td>
      Gateway timeout
      </td>
    </tr>
    <tr>
      <td>
        505
      </td>
      <td>
      HTTP version not supported
      </td>
    </tr>
  </tbody>
</table>


* 에러 코드(Exception)

<table>
  <thead>
    <tr>
    <th style="text-align:left">에러명</th>
      <th style="text-align:left">에러코드</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>RequestException</td>      
      <td>
        -1
      </td>
      <td>
      There was an ambiguous exception that occurred while handling your request.
      </td>
    </tr>
    <tr>
      <td> ConnectionErr</td>
      <td>
        -2
      </td>
      <td>
      In the event of a network problem (e.g. DNS failure, refused connection, etc)
      </td>
    </tr>
    <tr>
    <td> HTTPError
      <td>
        -3
      </td>
      <td>
      It will occur if the HTTP request returned an unsuccessful status code.
      </td>
    </tr>
    <tr>
    <td>URLRequired</td>
      <td>
        -4
      </td>
      <td>
      A valid URL is required to make a request.
      </td>
    </tr>
    <tr>
    <td>TooManyRedirects</td>
      <td>-5</td>
      <td>
      If a request exceeds the configured number of maximum redirections, a TooManyRedirects exception is raised.
      </td>
    </tr>
    <tr>
    <td>Timeout</td>
      <td>
        -6
      </td>
      <td>
      If a request times out, a Timeout exception is raised.
      </td>
    </tr>
  </tbody>
</table>
    
  