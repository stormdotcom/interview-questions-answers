### Modifiers with BEM (Block Element Modifier) Syntax

```css
.block {
  &-header {
    font-size: 20px;

    &-title {
      font-weight: bold;
    }
  }
}
```

### State-Specific Styles

```css
.button {
  background: lightblue;

  &:hover {
    color: white;
  }

  &-disabled {
    background: gray;
    pointer-events: none;
  }
}
```

### Nested Elements Inside States

```css
.card {
  border: 1px solid black;

  &:hover {
    .card-title {
      color: blue;
    }

    .card-content {
      font-size: 18px;
    }
  }
}
```

### Combining Pseudo-Elements

```css
.menu {
  &-item {
    color: black;

    &:hover::after {
      content: " →";
    }
  }
}
```

### Chaining Complex Selectors

```css
.nav {
  &-bar {
    display: flex;

    &-item {
      padding: 10px;

      &--active {
        font-weight: bold;

        &:hover {
          text-decoration: underline;
        }
      }
    }
  }
}
```
