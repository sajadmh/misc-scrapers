# Scraper Bookmarks (AKA Bookmarklets)


<h2>Instructions:</h2>

1. Create a new bookmark
2. Paste any one of the below snippets into the URL field
3. Go to the respective page and click the bookmark. If successful, a popup confirmation will be injected into the page and the result will be in the clipboard
4. To revise clipboard result according to the elements scraped, edit the <b>navigator.clipboard.writeText</b> section of the snippet



<h2><img src="https://raw.githubusercontent.com/sajadmh/Scraper-Hub/main/assets/Google-Calendar.png" style="height: 35px;"/>
Google Calendar Date, Time and Guestlist Scraper</h2>

```
javascript: (function scrapecal() { unformattedDate = document.querySelectorAll(".DN1TJ.fX8Pqc.CyPPBf")[0]?.innerText; date = unformattedDate.replace("⋅", " ⋅ "); children = []; invitees = document.querySelectorAll(".kMp0We.YaPvld.USzdTb.X4Mf1d>*"); invitees = Array.from(document.querySelectorAll('[role="treeitem"]')).filter(child=> { const ariaLabel=child.getAttribute("aria-label").toLowerCase(); return ariaLabel.includes("attending")&&!ariaLabel.includes("optional")&&!ariaLabel.includes("maybe") }); invitees.forEach(child => children.push(child.innerText)); children.forEach((child, i) => children[i] = child.replace(/,/g, "")); optionalWith = invitees.length?" with:</br>":""; delimiter = invitees.length?", <i>Title</i></br>":""; blob = new Blob(["<b>" + date + "</b>" + optionalWith + children.join(delimiter) + delimiter], { type: "text/html" }); data = [new ClipboardItem({ "text/html": blob })]; navigator.clipboard.write(data); console.log("Google Calendar Date (and Guest List) Scraped! (" + children + ")"); var el = document.createElement("div"), b = document.getElementsByTagName("body")[0], msg = "Copied to clipboard!"; el.style.position = "fixed"; el.style.zIndex = 99999; el.style.height = "25px"; el.style.width = "175px"; el.style.lineHeight = "25px"; el.style.textAlign = "center"; el.style.top = "10px"; el.style.left = "50%"; el.style.marginLeft = "-87px"; el.style.padding = "10px 10px"; el.style.fontFamily = "Roboto, Helvetica Neue, Helvetica, Arial, sans-serif"; el.style.fontSize = "15px"; el.style.fontWeight = "bold"; el.style.color = "#333333"; el.style.backgroundColor = "#FFFFFF"; el.style.border = "solid 1px #CECECE"; el.style.boxShadow = "0px 0px 6px #D6D6D6"; el.style.borderRadius = "9px"; if (document.hasFocus()) { return showMsg(); } function showMsg() { el.innerHTML = msg; b.appendChild(el); window.setTimeout(function() { el.remove(); }, 4250); } })();
```

Grabs the Google Calendar invite <b>date and time</b> and lists the <b>attending guests</b> in your clipboard (does not scrape declined, optional or unanswered guests). Only works on the calendar event popup on https://calendar.google.com/calendar/



<h2><img src="https://raw.githubusercontent.com/sajadmh/Scraper-Hub/main/assets/Google-Meet.png" style="height: 32px;"/>
Google Meet Link Scraper</h2>

```
javascript: (function scrapegmeet() { unformattedgMeet = document.querySelector(".EyDoae a").getAttribute("href"); gMeet = unformattedgMeet.slice(0, unformattedgMeet.lastIndexOf("?")); navigator.clipboard.writeText(gMeet); console.log("Google Meet Link Scraped!"); var el = document.createElement("div"), b = document.getElementsByTagName("body")[0], msg = "Copied to clipboard!"; el.style.position = "fixed"; el.style.zIndex = 99999; el.style.height = "25px"; el.style.width = "175px"; el.style.lineHeight = "25px"; el.style.textAlign = "center"; el.style.top = "10px"; el.style.left = "50%"; el.style.marginLeft = "-87px"; el.style.padding = "10px 10px"; el.style.fontFamily = "Roboto, Helvetica Neue, Helvetica, Arial, sans-serif"; el.style.fontSize = "15px"; el.style.fontWeight = "bold"; el.style.color = "#333333"; el.style.backgroundColor = "#FFFFFF"; el.style.border = "solid 1px #CECECE"; el.style.boxShadow = "0px 0px 6px #D6D6D6"; el.style.borderRadius = "9px"; if (document.hasFocus()) { return showMsg(); } function showMsg() { el.innerHTML = msg; b.appendChild(el); window.setTimeout(function() { el.remove(); }, 4250); } })();
```

Grabs the Google Meet <b>link</b> and puts it in your clipboard. Only works on the calendar event popup on https://calendar.google.com/calendar/





<h2><img src="https://raw.githubusercontent.com/sajadmh/Scraper-Hub/main/assets/WD-Scraper.png" style="height: 35px;"/>
Workday Scraper</h2>

```
javascript: (function scrapewd() { unformattedTitle = document.querySelector("[data-automation-id='workerProfileDetailsPanelName']")?.innerText; title = unformattedTitle.slice(0, unformattedTitle.lastIndexOf("(")); unformattedSubtitle = document.querySelector("[data-automation-id='workerProfileDetailsPanelSubtitleContainer']")?.innerText; unformattedSubtitle2 = unformattedSubtitle.slice(5); subtitle = unformattedSubtitle2.split(/^\S+\s+(.*)/).join(''); source = document.getElementById("56$581439")?.innerText; unformattedManager = document.getElementById("56$307577")?.innerText || ""; manager = unformattedManager.slice(0, unformattedManager.lastIndexOf(" (")); unformattedRecruiter = document.getElementById("56$307582")?.innerText || ""; recruiter = unformattedRecruiter.slice(0, unformattedRecruiter.lastIndexOf(" (")); var unformattedPhone = document.querySelectorAll("[data-automation-id='profileHeaderItem']")[0]?.innerText; unformattedPhone = unformattedPhone.replace("Jobs Applied to", ""); phone = unformattedPhone?.slice(13, unformattedPhone.lastIndexOf(" (")) || ""; unformattedEmail = document.querySelectorAll("[data-automation-id='profileHeaderItem']")[1]?.innerText || ""; email = unformattedEmail?.slice(6) || ""; tab = String.fromCodePoint(9); url = window.location.href; navigator.clipboard.writeText("=HYPERLINK(\"" + url + "\", \"" + title + "- " + subtitle + "\")" + tab + source + tab + "'" + phone + tab + email + tab + recruiter + tab + manager); console.log("Workday Scraped!"); var el = document.createElement("div"), b = document.getElementsByTagName("body")[0], msg = "Copied to clipboard!"; el.style.position = "fixed"; el.style.zIndex = 99999; el.style.height = "25px"; el.style.width = "175px"; el.style.lineHeight = "25px"; el.style.textAlign = "center"; el.style.top = "10px"; el.style.left = "50%"; el.style.marginLeft = "-87px"; el.style.padding = "10px 10px"; el.style.fontFamily = "Roboto, Helvetica Neue, Helvetica, Arial, sans-serif"; el.style.fontSize = "15px"; el.style.fontWeight = "bold"; el.style.color = "#333333"; el.style.backgroundColor = "#FFFFFF"; el.style.border = "solid 1px #CECECE"; el.style.boxShadow = "0px 0px 6px #D6D6D6"; el.style.borderRadius = "9px"; if (document.hasFocus()) { return showMsg(); } function showMsg() { el.innerHTML = msg; b.appendChild(el); window.setTimeout(function() { el.remove(); }, 4250); } })();
```

Grabs the Workday profile <b>title, phone number, email address, source, hiring manager name and recruiter name</b> and hyperlinks the <b>URL</b> in your clipboard. Only works on the summary page. Values are added to clipboard with tab spacing for column separation
	
