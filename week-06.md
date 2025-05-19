## Task 2

Using http://192.168.56.2 , we can run the webpage using any web browser. Initially, it will open index page. Upon clicking on button “Show date and time” we are getting the times and 
date which is depicts below:
![after_button_click](images/week6-task2-after_button_click.png)



## Task 3
**HTTP packet capture file**: [http-2291459.pcap](image/http-2291459.pcap). 

**ARP Table is shown below:**
![ARP_table](images/week6-task3-ARP_table.png)

## Task 4

 First, focus on the HTTP packets only by filtering for http,
![http-request](images/week6-task4.png)


**a) Understanding HTTP Request/Response Methods: Motivations, Requests, and Responses**

The image shows the below HTTP requests.  Here’s the analysis for each:
- 1) Time: 0.001271, GET / (HTTP/1.1 200 OK, 495 bytes) 
  - The user most likely entered the servers IP (192.168.56.2) or hostname in browser and requested the root of the server.
  - Browser initiated an HTTP GET to the root resource
  - The server response was 200, the request was delevered, and the server’s responded with data that client wanted, which in this case is a 495 byte HTML file (text/html) - likely the homepage.
- 2) Time: 0.043549, GET / (HTTP/1.1 200 OK, 618 bytes, text/html) 
  -  This looks like a subsequent request, which could be due to the browser doing a page refresh or navigating to the same root page again.
  - Another GET on the root ("/").
  - The server returned HTTP status code: 200 The response contained an HTML page of size 518 bytes The HTML page (text/html). The size difference of both (618 vs 495 bytes) could be one of an altered page, or maybe it was a different root resource.
- 3. Time: 0.073626, GET /styles.css (HTTP/1.1 200 OK, 389 bytes) 
  - The browser received and began to parse the root page’s HTML, and it found a link to a CSS file (styles. css) for styling the page.
  - HTTP GET for file "/styles. css".
  - The server returned the site with a 200 OK status, delivering a 389-byte CSS file (text/css)
- 4. Time: 0.115195, GET / (HTTP/1.1 200 OK, 1064 bytes, text/css) 
  - This is unusual because the request is for "/" but the response is a CSS file. It’s likely a misconfiguration on the server or an error in the capture. Normally, this would be triggered by the user accessing the root page again.
  - The root resource ("/") requested by an HTTP GET .
  - The server returned the site with a 200 OK status, but delivered a 1064-byte CSS file (text/css), which doesn’t match the expected HTML content.
- 5. Time: 1.919296, GET /2291459.html (HTTP/1.1 200 OK, 538 bytes) 
  - User probably followed to a particular page, clicking on a link on the home page, or enter the URL manually.
  - HTTP GET requests for the file "/2291459.html".
  - The server’s returned the 200 OK status, delivering a 538-byte HTML file (text/html), which is likely the user’s newly created web page.
  - Time: 1.921215, GET / (HTTP/1.1 200 OK, 104 bytes, text/html) 
  - This can be caused either by browser automatically refreshing the root page, or by user navigating back to the homepage.
  - HTTP GET request for the root resource ("/").
  - Server’s returned the 200 OK status, delivering a 104-byte HTML file (text/html), which is much smaller than previous root responses (possibly cached or a smaller version)
**b) First HTTP request is at Time 0.001271 (Frame 6). The 5 address values are:**
    1. Source IP Address (Host): 192.168.56.1 (client).
    2. Destination IP Address (Host): 192.168.56.2 (server).
    3. Source Port (Transport Protocol): 64749.
    4. Destination Port (Transport Protocol): 80 (standard HTTP port).
    5. Application Protocol: HTTP (Hypertext Transfer Protocol, as indicated by the GET / HTTP/1.1 request).
**c) Browser Behaviour Investigation: Is a Web Server Request Sent when Clicking the Time & dates Button?**
No, when we pressed button, our web browser probably didn’t send any requests to the web server’s.
Reason: It’s client-side handling of things, to put up the time and date of rendering on screen + use computer's time [which is done a lot of times with client-side scripting [in JavaScript, as used to get the local time on the browser from your system, with Date() function]]. No browser will do a new HTTP requests to the web server’s to perform this & write it the client because it can ask the user's device for the current date/time. There aren't any more HTTP requests in the packet capture that would be indicative of such an action, and that's not looking like any server request was made.
**d) Diagram of 22291459's HTTP-Request. Html**
HTTP request: GET /22291459.html HTTP/1.1. Let’s break down the packet structure, including header sizes and addresses.

![ARP_table](images/week6-task4-packet_diagram.png)
**Packet Diagram file**: [packet_diagram.drawio](image/week6-task4-packet_diagram.drawio). 

Size Break-down
  - Ethernet Header: 14 bytes 
  - IPv4 Header: 20 bytes 
  - TCP Header: 20 bytes 
  - HTTP Request: 484 bytes (as per the packet details: Len: 484 bytes).
  - Total Packet Size: 14 + 20 + 20 + 484 = 538 bytes.
Addresses Included
  - Ethernet Layer: MAC (Sources) (0a:00:27:00:00:09), and MAC (Destinations) (08:00:27:05:2b:d9).
  - IP Layer: IP (Sources) (192.168.56.1), IP (Destinations) (192.168.56.2).
  - TCP Layer: Port (Sources) (64749), Port (Destinations) (80).
  - HTTP Layer: Host header contains the destination host (192.168.56.2).
**e) Referrer for HTTP Request of 22291459.html**
**Referrer:** The HTTP request for /22291459. html contains Referer header. View packet details: Referer: http://192.168.56.2/. This means your referrer is the central page (/) most probably the index. Html.
**Identifies:** The Referer header indicates the source page of the request. On this occasion it indicates that the user being on http://192.168.56.2/ (that is the home page) accessed a link or specified in the address bar /22291459. html.
**How Web Servers Work With This Data**
  - Analytics: Servers use referrers to see where users are coming from (i.e. which page they last visited that resulted in the current request).
  - Security: It can help detect suspicious activity, like cross-site request forgery (CSRF), by verifying the request’s origin.
  - User Experience: The server can modify response according to the referrer (e.g. showing a “back to home” link if the user came from the home page).
**f) Server learned data on the web browser**
Headers The HTTP-request includes the User-Agent header, which discloses the browser of the user. The User-Agent string itself doesn’t appear in the capture, but if you look at the details of the HTTP packet at the right of the screenshot, you can see part of the HTTP request:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36 Edge/126.0.0.0
Information Learned by the Server:
  - Browser Name: Microsoft Edge (indicated by "Edge/126").
  - Browser Version: 126.0.0.0 (from "Edge/126.0.0.0").
  - Rendering Engine: AppleWebKit/537.36 (KHTML, like Gecko) – indicates the browser uses WebKit/Blink rendering engine.
  - OS: Windows 11 (from "Windows NT 11.0").
  - Architecture: 64-bit (from "Win64; x64").
  - Additional Compatibility: The "Mozilla/5.0" and "Safari/537.36" indicate compatibility identifiers for historical web compatibility.
The server can use this information to:
  - Optimize content delivery (serve browser-specific CSS or JavaScript).
  - Track browser usage statistics for analytics.
  - Identify potential compatibility issues with certain browser versions.
**g)  The HTTP version used is HTTP/1.1, and the transport protocols is TCP.**
**h)  Packets involved in connection setup (TCP 3-ways handshakes):**
  - Packet 1 (SYN): 192.168.56.1 → 192.168.56.2 [start of the handshake]
  - Packet 4 (SYN-ACK): 192.168.56.2 → 192.168.56.1 [It response from the server]
  - Packet 5 (ACK): 192.168.56.1 → 192.168.56.2 [completes the handshake]
Packet 2 & 3 are ARP packet, so this are unrelated to the TCP handshake.
Now lets count the times among the beginning of connections setup and the data transfers:
First HTTP requests (data transfer) occurs in Packet 6 at 0.001271 seconds. The connection setup starts at Packet 1 (0.000000 seconds). The total time is 0.001271 seconds (≈1.27 milliseconds).
    • Connection establishment packets:1, 4, and 5. 
    • Time from opening a connection to the first data-cards cop-out: 1.271 ms.
i)  
In the TCP protocol, ACK (acknowledgements) is sent to acknowledge receipt of data. From the packet capture:
    • Packet 5: "[ACK] Seq=1 Ack=1 Win=65280 Len=0" – This is parts of the TCP handshakes, acknowledging the SYN-ACK.
    • Packet 7: "[ACK] Seq=1 Ack=442 Win=64808 Len=0" – Acknowledges data from the server.
    • Packet 9: "[ACK] Seq=442 Ack=42 Win=65280 Len=4" – Acknowledges receipt of an HTTP response.
    • Packet 11: "[ACK] Seq=686 Ack=777 Win=64768 Len=0" – Acknowledges more data.
    • Packet 13: "[ACK] Seq=777 Ack=647 Win=64768 Len=0" – Another acknowledgment.
    • Packet 15: "[ACK] Seq=777 Ack=1657 Win=65280 Len=0" – Acknowledges further data.
    • Packet 17: "[ACK] Seq=1657 Ack=1261 Win=64080 Len=0" – Acknowledges additional data.
    • Packet 19: "[ACK] Seq=1261 Ack=3158 Win=65280 Len=0" – Acknowledges more data.
    • Packet 21: "[ACK] Seq=3158 Ack=3208 Win=65280 Len=0" – Final acknowledgment in this capture.
These packets (5, 7, 9, 11, 13, 15, 17, 19, 21) are acknowledgements.
The usual acknowledgment in TCP is:
    • On receiving a segment: TCP ACKs segments that are received correctly. For instance, after the client has issued an HTTP GET request (Packet 10) the server responds with data (Packet 12), followed by an ACK (Packet 13) from the client, acknowledging the received data.
    • During the TCP handshake: As seen in Packet 5, an ACK is sent to complete the three-way handshake.
    • After a certain amount of data: TCP can be using delayed ACKs, meaning an ACK is sent after a predefined amount of data comes in (e.g., two segments) or a timeout (usually 200 ms) occurs to minimize overhead.
    • To acknowledge out-of-order packets or retransmissions: If packets are received out of order, TCP uses selective ACKs (SACK) to acknowledge specific segments, as seen in the "SACK_PERM" option in the packets.
In this capture, ACKs are sent after each HTTP request/response exchange (e.g., Packet 11 after Packet 10's GET request and Packet 12's response) and during the connection setup.

Task-5

The following Screenshot of the cookies set by BBC website (bbc. com) in the Storage section of the browser's Application tab.

Cookie are a tiny piece of information websites store on a users computer to keep track of activity, such as remembering preferences or managing sessions. Here is a guide to the kinds of information generally found in cookies like those listed; these are cookies measuring just 30 days of activity.
    1. Session and Authentication Data: 
        ◦ Cookies like ckns_explicit or ckns_policy often store user consent for cookie usage or privacy policies.
        ◦ sp_su (highlighted) might indicate a user ID or session token, used to maintain a logged-in state or track a specific user session.
    2. Tracking and Analytics: 
        ◦ Cookies such as atid, atuserid, or atuserid are typically used for tracking user behavior across the site. These might store unique identifiers to monitor how users interact with the website, often for analytics purposes (e.g., which pages are visited).
        ◦ chartbeat2 and chartbeat4 is related to Chartbeat, a real time analytics service. Cookies for monitoring engagement and interaction with specific elements on the page.
    3. Personalization: 
        ◦ Cookies like pid, pctx, or pcus might store user preferences or personalized settings, such as location, language, or content recommendations. For example, pid could be a personalization ID to tailor news content based on user interests.
    4. Advertising: 
    • Cookies such as ad_id or those with long alphanumeric values (e.g., J62H5...) are often tied to advertising networks. They store data to deliver targeted ads, track ad impressions, or measure ad performance.
    • gads likely relates to Google Ads, storing information for ad targeting or conversion tracking.
    5. Security and Functionality: 
        ◦ The Secure flag (appearing on some cookies), which tells the browser to send the cookie over HTTPS, to make it more secure. 
        ◦ Http Only (present as well) prevents client side scripts from reading the cookie, reducing XSS risk. 
        ◦ SameSite settings (for example, Lax or None) determine how cookies are sent in cross-site requests, which prevents cross-site request forgery (CSRF) attacks.
    6. Expiration and Persistence: 
    • The Expires / Max-Age column shows when cookies expire. For example, most cookies here expire between 2025-05-18 and 2026-11-14, meaning they persist for tracking or functionality over that period.
    • Some cookies, like ar_debug, have a shorter lifespan (e.g., 2025-06-17), possibly for temporary debugging purposes.
    7. Size and Priority: 
    • The Size column indicates the cookie's data size in bytes (e.g., 177 bytes for cf_bm). Smaller cookies are typically for simple flags, while larger ones might store more complex data like encoded user profiles.
    • Priority (e.g., Medium, Lax) reflects the cookie's importance for browser handling, though this is less about the data type and more about browser behavior.
In summary, these cookies contain a mix of session management, user tracking, personalization, advertising, and security-related data. They help the website function smoothly, improve user experience, and provide analytics or targeted ads, while also implementing security measures to protect user data.




References
OpenWrt Forum. “How to Create Custom Page on Openwrt Luci.” OpenWrt Forum, 15 Jan. 2020, forum.openwrt.org/t/how-to-create-custom-page-on-openwrt-luci/52777. Accessed 18 May 2025.
OpenWRT, in. “Stack Overflow.” Stack Overflow, 24 Apr. 2017, stackoverflow.com/questions/43581169/how-to-add-new-pages-in-openwrt-luci-web-interface. 
info@spotlightcybersecurity.com. “Network Traffic Inspection - TCPDUMP on OpenWRT - Spotlight Cybersecurity.” Spotlightcybersecurity.com, 10 Oct. 2018, spotlightcybersecurity.com/tcpdump-on-openwrt.html.
Garn, Damon . “Examine a Captured Packet Using Wireshark | Techtarget.” Networking, 17 Apr. 2023, www.techtarget.com/searchnetworking/tutorial/Examine-a-captured-packet-using-Wireshark.
MSEdgeTeam. “View, Edit, and Delete Cookies - Microsoft Edge Developer Documentation.” Microsoft.com, 7 Dec. 2023, learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/storage/cookies.




![ARP_table](images/week6-task3-ARP_table.png)


![ARP_table](images/week6-task3-ARP_table.png)

