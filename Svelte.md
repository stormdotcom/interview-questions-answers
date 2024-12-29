# Svelte Interview Questions: Essential Topics

## 1. General Svelte Basics

### **Q1: What is Svelte, and how does it differ from frameworks like React or Vue?**
- **Answer**: Svelte is a frontend framework that shifts much of the work to compile time, generating vanilla JavaScript code at build time. Unlike React or Vue, which use a virtual DOM, Svelte updates the DOM directly for better performance.

---

### **Q2: What are Svelte components?**
- **Answer**: Svelte components are self-contained blocks of functionality (HTML, CSS, and JavaScript) encapsulated in `.svelte` files.

---

### **Q3: How do you create and use a Svelte component?**
```svelte
<!-- Button.svelte -->
<script>
  export let label = 'Click Me';
</script>

<button>{label}</button>

// Usage in Parent Component
<script>
  import Button from './Button.svelte';
</script>

<Button label="Submit" />
```

---

## 2. Reactivity in Svelte

### **Q4: How does reactivity work in Svelte?**
- **Answer**: Reactivity is achieved by directly updating variables. Svelte automatically tracks changes and updates the DOM.

---

### **Q5: What is the `$:` reactive statement in Svelte?**
- **Answer**: `$:` is used for reactive declarations, recalculating values when dependencies change.

```svelte
<script>
  let count = 0;

  $: double = count * 2; // Reactive statement
</script>

<p>Count: {count}</p>
<p>Double: {double}</p>
<button on:click={() => count++}>Increment</button>
```

---

## 3. Props and State Management

### **Q6: How do you pass and receive props in Svelte?**
- **Answer**: Props are passed from a parent component and declared using `export`.

```svelte
<script>
  export let name;
</script>

<p>Hello, {name}!</p>
```

---

### **Q7: What are writable stores in Svelte, and how are they used?**
- **Answer**: Stores are a reactive way to share state between components.

```javascript
// store.js
import { writable } from 'svelte/store';

export const count = writable(0);
```

```svelte
<!-- App.svelte -->
<script>
  import { count } from './store.js';
</script>

<p>{$count}</p>
<button on:click={() => $count++}>Increment</button>
```

---

## 4. Lifecycle and Events

### **Q8: What are the Svelte lifecycle hooks?**
- **Answer**: Svelte provides hooks like `onMount`, `beforeUpdate`, and `onDestroy` to manage component lifecycle.

```svelte
<script>
  import { onMount, onDestroy } from 'svelte';

  let timer;

  onMount(() => {
    timer = setInterval(() => console.log('Tick'), 1000);
  });

  onDestroy(() => {
    clearInterval(timer);
  });
</script>
```

---

### **Q9: How do you handle events in Svelte?**
- **Answer**: Svelte uses the `on:` directive for event handling.

```svelte
<button on:click={() => console.log('Button clicked!')}>Click Me</button>
```

---

## 5. Advanced Topics

### **Q10: What are slots in Svelte?**
- **Answer**: Slots allow you to pass content into a component from its parent.

```svelte
<!-- Card.svelte -->
<div class="card">
  <slot name="header"></slot>
  <slot></slot>
</div>
```

```svelte
<!-- App.svelte -->
<Card>
  <h1 slot="header">Header Content</h1>
  <p>Main Content</p>
</Card>
```

---

### **Q11: How does Svelte handle transitions and animations?**
- **Answer**: Svelte provides built-in directives like `transition:fade` and functions like `animate` for animations.

```svelte
<script>
  import { fade } from 'svelte/transition';
  let visible = true;
</script>

<button on:click={() => (visible = !visible)}>Toggle</button>
{#if visible}
  <p transition:fade>This text will fade in and out</p>
{/if}
```

---

### **Q12: What is the purpose of `context` in Svelte?**
- **Answer**: `context` provides a way to pass data deeply through the component tree without props.

```svelte
// Parent.svelte
<script>
  import { setContext } from 'svelte';
  setContext('key', 'value');
</script>
<Child />

// Child.svelte
<script>
  import { getContext } from 'svelte';
  const value = getContext('key');
</script>
<p>{value}</p>
```

