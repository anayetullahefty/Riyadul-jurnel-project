# Week 6 Tasks

## Task 2

Using `http://192.168.56.2`, we can access the webpage via any web browser. Initially, it opens the index page. Upon clicking the "Show date and time" button, the date and time are displayed as shown below:

![After Button Click](images/week6-task2-after_button_click.png)

## Task 3

**HTTP Packet Capture File**: [http-2291459.pcap](image/http-2291459.pcap)

**ARP Table**:

![ARP Table](images/week6-task3-ARP_table.png)

## Task 4

Filter for HTTP packets only to focus on HTTP traffic:

![HTTP Request](images/week6-task4.png)

#### a) Understanding HTTP Request/Response Methods: Motivations, Requests, and Responses

The image shows the following HTTP requests. Here’s the analysis for each:

1. **Time: 0.001271, GET / (HTTP/1.1 200 OK, 495 bytes)**
   - The user likely entered the server’s IP (`192.168.56.2`) or hostname in the browser to request the root page.
   - Browser initiated an HTTP GET to the root resource (`/`).
   - The server responded with a `200 OK` status, delivering a 495-byte HTML file (`text/html`), likely the homepage.

2. **Time: 0.043549, GET / (HTTP/1.1 200 OK, 618 bytes, text/html)**
   - This appears to be a subsequent request, possibly due to a page refresh or navigating to the same root page again.
   - Another GET request for the root (`/`).
   - The server returned a `200 OK` status with a 618-byte HTML page (`text/html`). The size difference (618 vs. 495 bytes) could indicate an altered page or a different root resource.

3. **Time: 0.073626, GET /styles.css (HTTP/1.1 200 OK, 389 bytes)**
   - The browser parsed the root page’s HTML and found a link to a CSS file (`styles.css`) for styling.
   - HTTP GET request for `/styles.css`.
   - The server returned a `200 OK` status, delivering a 389-byte CSS file (`text/css`).

4. **Time: 0.115195, GET / (HTTP/1.1 200 OK, 1064 bytes, text/css)**
   - This is unusual as the request is for `/` but the response is a CSS file. It’s likely a server misconfiguration or capture error.
   - HTTP GET request for the root resource (`/`).
   - The server returned a `200 OK` status but delivered a 1064-byte CSS file (`text/css`), which doesn’t match the expected HTML content.

5. **Time: 1.919296, GET /2291459.html (HTTP/1.1 200 OK, 538 bytes)**
   - The user likely clicked a link on the homepage or manually entered the URL.
   - HTTP GET request for `/2291459.html`.
   - The server returned a `200 OK` status, delivering a 538-byte HTML file (`text/html`), likely a user-created webpage.

6. **Time: 1.921215, GET / (HTTP/1.1 200 OK, 104 bytes, text/html)**
   - This could be due to the browser automatically refreshing the root page or the user navigating back to the homepage.
   - HTTP GET request for the root resource (`/`).
   - The server returned a `200 OK` status, delivering a 104-byte HTML file (`text/html`), smaller than previous root responses (possibly cached or a smaller version).

#### b) First HTTP Request Details

The first HTTP request occurs at **Time: 0.001271 (Frame 6)**. The five address values are:

1. **Source IP Address (Host)**: `192.168.56.1` (client)
2. **Destination IP Address (Host)**: `192.168.56.2` (server)
3. **Source Port (Transport Protocol)**: `64749`
4. **Destination Port (Transport Protocol)**: `80` (standard HTTP port)
5. **Application Protocol**: HTTP (indicated by the `GET / HTTP/1.1` request)

#### c) Browser Behavior: Web Server Request on Clicking "Time & Date" Button

No, clicking the "Time & Date" button likely does not trigger a web server request. 

**Reason**: The date and time display is handled client-side, likely using JavaScript (e.g., the `Date()` function) to retrieve the local system credit: time. No additional HTTP requests appear in the packet capture to indicate a server request for this action.

#### d) Diagram of `/2291459.html` HTTP Request

**HTTP Request**: `GET /2291459.html HTTP/1.1`

**Packet Diagram File**: [packet_diagram.drawio](image/week6-task4-packet_diagram.drawio)

![Packet Diagram](images/week6-task4-packet_diagram.png)

**Size Breakdown**:

- **Ethernet Header**: 14 bytes
- **IPv4 Header**: 20 bytes
- **TCP Header**: 20 bytes
- **HTTP Request**: 484 bytes (as per packet details: Len: 484 bytes)
- **Total Packet Size**: 14 + 20 + 20 + 484 = 538 bytes

**Addresses Included**:

- **Ethernet Layer**: Source MAC: `0a:00:27:00:00:09`, Destination MAC: `08:00:27:05:2b:d9`
- **IP Layer**: Source IP: `192.168.56.1`, Destination IP: `192.168.56.2`
- **TCP Layer**: Source Port: `64749`, Destination Port: `80`
- **HTTP Layer**: Host header contains the destination host (`192.168.56.2`)

#### e) Referrer for `/2291459.html` HTTP Request

**Referrer**: The HTTP request for `/2291459.html` includes a `Referer` header: `http://192.168.56.2/`.

**Identifies**: The `Referer` header indicates the source page of the request. Here, it shows the user was on the homepage (`http://192.168.56.2/`) and either clicked a link or entered `/2291459.html` manually.

**How Web Servers Use This Data**:

- **Analytics**: Tracks where users are coming from (e.g., which page led to the current request).
- **Security**: Helps detect suspicious activity, like cross-site request forgery (CSRF), by verifying the request’s origin.
- **User Experience**: Can modify responses based on the referrer (e.g., adding a “back to home” link).

#### f) Server-Learned Data About the Web Browser

The HTTP request includes a `User-Agent` header, revealing browser details. From the packet capture:

**User-Agent**: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36 Edge/126.0.0.0`

**Information Learned**:

- **Browser Name**: Microsoft Edge (`Edge/126`)
- **Browser Version**: `126.0.0.0`
- **Rendering Engine**: WebKit/Blink (`AppleWebKit/537. skis36`)
- **OS**: Windows 10 (`Windows NT 10.0`)
- **Architecture**: 64-bit (`Win64; x64`)
- **Compatibility**: `Mozilla/5.0` and `Safari/537.36` are for historical web compatibility

**Server Uses**:

- Optimize content delivery (e.g., browser-specific CSS/JavaScript).
- Track browser usage for analytics.
- Identify compatibility issues with specific browser versions.

#### g) HTTP Version and Transport Protocol

- **HTTP Version**: `HTTP/1.1`
- **Transport Protocol**: `TCP`

#### h) Packets Involved in TCP Connection Setup (3-Way Handshake)

- **Packet 1 (SYN)**: `192.168.56.1 → 192.168.56.2` (start of handshake)
- **Packet 4 (SYN-ACK)**: `192.168.56.2 → 192.168.56.1` (server response)
- **Packet 5 (ACK)**: `192.168.56.1 → 192.168.56.2` (completes handshake)

**Note**: Packets 2 and 3 are ARP packets, unrelated to the TCP handshake.

**Time Calculation**:

- First HTTP request (data transfer): Packet 6 at `0.001271` seconds
- Connection setup starts: Packet 1 at `0.000000` seconds
- **Total Time**: `0.001271` seconds (≈1.27 milliseconds)

**Connection Establishment Packets**: 1, 4, 5

**Time from Connection to Data Transfer**: 1.271 ms

#### i) TCP Acknowledgments (ACKs)

In TCP, ACKs confirm receipt of data. From the packet capture:

- **Packet 5**: `[ACK] Seq=1 Ack=1 Win=65280 Len=0` – Part of TCP handshake, acknowledging SYN-ACK.
- **Packet 7**: `[ACK] Seq=1 Ack=442 Win=64808 Len=0` – Acknowledges server data.
- **Packet 9**: `[ACK] Seq=442 Ack=42 Win=65280 Len=4` – Acknowledges HTTP response.
- **Packet 11**: `[ACK] Seq=686 Ack=777 Win=64768 Len=0` – Acknowledges more data.
- **Packet 13**: `[ACK] Seq=777 Ack=647 Win=64768 Len=0` – Another acknowledgment.
- **Packet 15**: `[ACK] Seq=777 Ack=1657 Win=65280 Len=0` – Acknowledges further data.
- **Packet 17**: `[ACK] Seq=1657 Ack=1261 Win=64080 Len=0` – Acknowledges additional data.
- **Packet 19**: `[ACK] Seq=1261 Ack=3158 Win=65280 Len=0` – Acknowledges more data.
- **Packet 21**: `[ACK] Seq=3158 Ack=3208 Win=65280 Len=0` – Final acknowledgment.

**ACK Behavior**:

- **On Segment Receipt**: TCP ACKölker: s correctly received segments (e.g., Packet 13 acknowledges Packet 12’s response after Packet 10’s GET request).
- **During Handshake**: Packet 5 completes the 3-way handshake.
- **Delayed ACKs**: TCP may delay ACKs (e.g., after two segments or a 200 ms timeout) to reduce overhead.
- **Selective ACKs (SACK)**: Used for out-of-order packets or retransmissions, as seen with the `SACK_PERM` option.

## Task 5

**Screenshot**: Cookies set by the BBC website (`bbc.com`) in the browser’s Application tab (Storage section).

Cookies are small pieces of data stored on a user’s computer to track activity, manage sessions, or remember preferences. Below is an analysis of the types of information typically found in cookies like those listed (covering 30 days of activity):

1. **Session and Authentication Data**:
   - Cookies like `ckns_explicit` or `ckns_policy` store user consent for cookie usage or privacy policies.
   - `sp_su` (highlighted) may indicate a user ID or session token for maintaining logged-in states or tracking sessions.

2. **Tracking and Analytics**:
   - Cookies like `atid`, `atuserid`, or `atuserid` track user behavior across the site, storing unique identifiers for analytics (e.g., page visits).
   - `chartbeat2` and `chartbeat4` relate to Chartbeat, a real-time analytics service, monitoring engagement with page elements.

3. **Personalization**:
   - Cookies like `pid`, `pctx`, or `pcus` store preferences or settings (e.g., location, language, content recommendations). `pid` may be a personalization ID for tailored news content.

4. **Advertising**:
   - Cookies like `ad_id` or long alphanumeric values (e.g., `J62H5...`) are tied to advertising networks, delivering targeted ads or tracking impressions/performance.
   - `gads` likely relates to Google Ads for ad targeting or conversion tracking.

5. **Security and Functionality**:
   - **Secure Flag**: Ensures cookies are sent over HTTPS for security.
   - **HttpOnly**: Prevents client-side scripts from accessing cookies, reducing XSS risks.
   - **SameSite Settings** (e.g., `Lax` or `None`): Controls cookie behavior in cross-site requests to prevent CSRF attacks.

6. **Expiration and Persistence**:
   - Cookies expire between `2025-05-18` and `2026-11-14`, persisting for tracking or functionality.
   - Some, like `ar_debug`, have shorter lifespans (e.g., `2025-06-17`) for temporary debugging.

7. **Size and Priority**:
   - Cookie sizes (e.g., 177 bytes for `cf_bm`) indicate simple flags or complex data like encoded profiles.
   - Priority (e.g., `Medium`, `Lax`) reflects browser handling importance.

**Summary**: These cookies support session management, user tracking, personalization, advertising, and security. They enhance website functionality, improve user experience, provide analytics, deliver targeted ads, and implement security measures.

## References

- OpenWrt Forum. “How to Create Custom Page on OpenWrt LuCI.” *OpenWrt Forum*, 15 Jan. 2020, <https://forum.openwrt.org/t/how-to-create-custom-page-on-openwrt-luci/52777>. Accessed 18 May 2025.
- OpenWRT. “Stack Overflow.” *Stack Overflow*, 24 Apr. 2017, <https://stackoverflow.com/questions/43581169/how-to-add-new-pages-in-openwrt-luci-web-interface>.
- Spotlight Cybersecurity. “Network Traffic Inspection - TCPDUMP on OpenWRT.” *Spotlightcybersecurity.com*, 10 Oct. 2018, <https://spotlightcybersecurity.com/tcpdump-on-openwrt.html>.
- Garn, Damon. “Examine a Captured Packet Using Wireshark.” *TechTarget*, 17 Apr. 2023, <https://www.techtarget.com/searchnetworking/tutorial/Examine-a-captured-packet-using-Wireshark>.
- MSEdgeTeam. “View, Edit, and Delete Cookies - Microsoft Edge Developer Documentation.” *Microsoft.com*, 7 Dec. 2023, <https://learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/storage/cookies>.
