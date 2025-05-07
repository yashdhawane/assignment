# Hypermart Checkout Assignment

This README will guide you step by step through the code for the Hypermart Checkout Assignment. By the end, you’ll understand how the HTML structure, CSS styles, and JavaScript logic all work together to create a dynamic checkout queue system.

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Getting Started](#getting-started)
3. [File Structure](#file-structure)
4. [HTML Explained](#html-explained)
5. [CSS Explained](#css-explained)
6. [JavaScript Explained](#javascript-explained)
   - [Constants & Initialization](#constants--initialization)
   - [Rendering the UI](#rendering-the-ui)
   - [Adding a Customer](#adding-a-customer)
   - [Event Listeners](#event-listeners)
7. [How It All Works Together](#how-it-all-works-together)
8. [Next Steps](#next-steps)

---

## Project Overview
This small web app simulates multiple checkout counters (queues) in a grocery store. When a customer with a certain number of items arrives, the script automatically assigns them to the *least busy* counter. Each counter’s queue and total item count update in real time.

## Getting Started
1. Clone or download the repository.
2. Open `index.html` in your browser.
3. Enter the number of items for each new customer and click **Add Customer**.
4. Watch how customers get assigned to the shortest queue.

## File Structure
```
/ (project root)
│
├── index.html      # Contains HTML, CSS, and JS
└── (optional splits)
    ├── styles.css  # CSS only
    └── script.js   # JS only
```

## HTML Explained
The HTML defines the page structure:

```html
<!DOCTYPE html>
<html lang="en">
<head> … </head>
<body>
  <h1>Hypermart Checkout Queues</h1>

  <div class="controls">
    <input id="item-count" placeholder="# of items" />
    <button id="add-btn">Add Customer</button>
  </div>

  <div id="checkout-container"></div>
</body>
</html>
```
- **`<h1>`**: Page title.
- **`.controls`**: Contains an input field (customer items) and a button.
- **`#checkout-container`**: Empty placeholder where checkout lanes render.

## CSS Explained
Inside `<style>` (or `styles.css`):
- **Body**: Light background, simple font, padding.
- **Controls**: Center-aligned input and button styling.
- **Checkout Grid**: A responsive grid (`grid-template-columns`) that adapts to screen size.
- **`.checkout` cards**: White background, rounded corners, subtle shadow, padding.
- **`.queue` list**: Unstyled list with grey backgrounds for each customer.

## JavaScript Explained
All the dynamic behavior lives in the `<script>` (or `script.js`). Let’s break it down.

### Constants & Initialization
```js
const NUM_CHECKOUTS = 3;
const checkouts = Array.from(
  { length: NUM_CHECKOUTS },
  () => ({ items: [], total: 0 })
);
const container = document.getElementById('checkout-container');
const input = document.getElementById('item-count');
const addBtn = document.getElementById('add-btn');
```
- **`NUM_CHECKOUTS`**: Total checkout lanes.
- **`checkouts`**: An array of length `NUM_CHECKOUTS`. Each element is an object:
  ```js
  { items: [], total: 0 }
  ```
  - `items` holds customer item counts in queue order.
  - `total` is the sum of all items in that lane.
- **DOM References**: Grab the container, input field, and button for later use.

### Rendering the UI
```js
function render() {
  container.innerHTML = '';
  checkouts.forEach((checkout, index) => {
    // Create card, title, list, and total elements
    container.appendChild(div);
  });
}
```
- **Clearing**: `container.innerHTML = ''` removes old content.
- **Loop**: For each checkout lane, build a `<div>` with:
  1. `<h2>` showing “Checkout X”.
  2. `<ul>` listing each customer’s item count.
  3. `<div>` displaying the lane’s total items.
- **Append**: Add each lane div to the page.

### Adding a Customer
```js
function addCustomer(count) {
  // 1. Find the lane with the smallest total
  // 2. Push the new count into items
  // 3. Add count to total
  render();
}
```
- **Find min**: Iterate through `checkouts` to pick the lane whose `total` is lowest.
- **Assign**: Add the customer’s item count to that lane’s `items` array and update `total`.
- **Re-render**: Update the UI to reflect changes.

### Event Listeners
```js
addBtn.addEventListener('click', () => {
  const count = parseInt(input.value, 10);
  if (isNaN(count) || count < 1) {
    alert('Please enter a valid number of items (>=1).');
    return;
  }
  addCustomer(count);
  input.value = '';
  input.focus();
});
```
- **Click**: When the user clicks **Add Customer**:
  1. Read and parse the input value.
  2. Validate: Must be a number ≥ 1.
  3. On success, call `addCustomer()`.
  4. Clear and refocus the input field.

## How It All Works Together
1. The page loads with 3 empty checkout lanes.
2. User enters an item count and clicks **Add Customer**.
3. JavaScript finds the shortest lane, updates its data, and re-renders.
4. Each lane’s queue and total update immediately in the UI.

This simple approach scales: increase `NUM_CHECKOUTS`, and the grid and logic adapt automatically.



---


