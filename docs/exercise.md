---
title: 📝 HTML & Markdown Exercises
---

## Exercise 1: Basic HTML Form

**Objective:** สร้างแบบฟอร์มการติดต่อข้อมูลง่าย ๆ

**Requirements:**
- ใช้ `<form>` element
- มี input fields สำหรับ:
  - ชื่อ (text input)
  - อีเมล (email input)
  - เบอร์โทรศัพท์ (tel input)
  - ข้อความ (textarea)
- มี submit button

**Example Output:**
```html
<form>
  <fieldset>
    <legend>Contact Form</legend>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    
    <label for="phone">Phone:</label>
    <input type="tel" id="phone" name="phone">
    
    <label for="message">Message:</label>
    <textarea id="message" name="message"></textarea>
    
    <input type="submit" value="Send">
  </fieldset>
</form>
```

---

## Exercise 2: Product Card with HTML & Styling

**Objective:** สร้างการ์ดสินค้า (Product Card)

**Requirements:**
- ใช้ `<article>` หรือ `<div>` สำหรับ container
- มี image (`<img>`)
- มี product name (heading)
- มี description
- มี price
- มี "Add to Cart" button

**Example Output:**
```html
<article class="product-card">
  <img src="https://via.placeholder.com/300" alt="Product Image">
  <h3>Premium Widget</h3>
  <p>High-quality widget for everyday use</p>
  <meter min="0" max="5" value="4"></meter>
  <p><strong>$29.99</strong></p>
  <button>Add to Cart</button>
</article>
```

---

## Exercise 3: Markdown Documentation

**Objective:** เขียน documentation ในรูปแบบ Markdown

**Requirements:**
- มี heading หลัก (H1)
- มี sub-headings (H2, H3)
- มี list (ordered & unordered)
- มี code block
- มี blockquote
- มี link อย่างน้อย 1 อัน

**Example Output:**
````markdown
# Python Getting Started

## Installation

Follow these steps:

1. Download Python from [python.org](https://python.org)
2. Run the installer
3. Verify installation

## Basic Syntax

### Variables

```python
name = "John"
age = 25
```

### Data Types

- Strings
- Numbers
- Lists
- Dictionaries

> "Python is easy to learn and powerful to use." — Guido van Rossum

## Common Commands

| Command | Purpose |
|---------|---------|
| `python --version` | Check version |
| `pip install` | Install packages |
````

---

## Exercise 4: Interactive HTML with Details Element

**Objective:** สร้างส่วน FAQ โดยใช้ `<details>` element

**Requirements:**
- มี `<details>` elements อย่างน้อย 3 ตัว
- แต่ละตัวมี `<summary>`
- ตัวแรกต้องมี `open` attribute
- มี content ในแต่ละ details

**Example Output:**
```html
<section>
  <h2>Frequently Asked Questions</h2>
  
  <details open>
    <summary>What is this product?</summary>
    <p>This is a premium widget designed for professional users.</p>
  </details>
  
  <details>
    <summary>How do I install it?</summary>
    <p>Simply download and follow the installation wizard.</p>
  </details>
  
  <details>
    <summary>What is the warranty?</summary>
    <p>We offer a 2-year manufacturer's warranty.</p>
  </details>
</section>
```

---

## Exercise 5: Semantic HTML Article

**Objective:** สร้างบทความข่าวหรือบล็อก

**Requirements:**
- ใช้ `<article>` element
- มี `<header>` กับ `<footer>`
- มี `<h1>` สำหรับชื่อเรื่อง
- มี `<time>` element
- มี `<p>` paragraphs อย่างน้อย 3 ตัว
- มี `<figure>` พร้อม `<figcaption>`

**Example Output:**
```html
<article>
  <header>
    <h1>Web Design Trends in 2025</h1>
    <p>Posted on <time datetime="2025-08-16">August 16, 2025</time></p>
  </header>
  
  <p>The web design industry continues to evolve...</p>
  
  <figure>
    <img src="https://via.placeholder.com/600" alt="Design trends">
    <figcaption>Modern design principles (Source: Design Weekly)</figcaption>
  </figure>
  
  <p>Dark mode has become increasingly popular...</p>
  
  <footer>
    <p>Written by <strong>Jane Designer</strong></p>
  </footer>
</article>
```

---

## Exercise 6: Comparison Table

**Objective:** สร้างตารางเปรียบเทียบ

**Requirements:**
- ใช้ `<table>` element พร้อม `<thead>`, `<tbody>`
- มี `<caption>` (optional)
- อย่างน้อย 4 rows × 4 columns
- สามารถใช้ `<th>` สำหรับ headers

**Example Output:**
```html
<table>
  <caption>Plan Comparison</caption>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Basic</th>
      <th>Pro</th>
      <th>Enterprise</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Users</td>
      <td>1</td>
      <td>5</td>
      <td>Unlimited</td>
    </tr>
    <tr>
      <td>Storage</td>
      <td>10GB</td>
      <td>100GB</td>
      <td>1TB</td>
    </tr>
    <tr>
      <td>Support</td>
      <td>Email</td>
      <td>Priority</td>
      <td>24/7 Phone</td>
    </tr>
  </tbody>
</table>
```

---

## Challenge: Combine All Skills

**Objective:** รวมทักษะทั้งหมดเพื่อสร้างหน้าเว็บ

สร้างหน้าเว็บ `challenge.md` ที่รวม:
- Markdown documentation ที่อธิบาย project
- HTML form สำหรับ contact
- HTML table สำหรับแสดงข้อมูล
- HTML details/accordion สำหรับ FAQ
- Product cards
- Images และ links

---

## Tips & Resources

- 📖 [MDN Web Docs - HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
- 📖 [MDN Web Docs - Markdown](https://developer.mozilla.org/en-US/docs/MDN/Markdown_contents)
- 🎨 [Placeholder Images](https://via.placeholder.com/)
- ✅ [HTML Validator](https://validator.w3.org/)

---

Good luck! 🚀
