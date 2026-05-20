# 4.4 Styling

## Inline Styles

```javascript
function Box() {
  const styles = {
    container: {
      backgroundColor: 'blue',
      padding: '20px',
      borderRadius: '5px'
    },
    text: {
      color: 'white',
      fontSize: '18px'
    }
  };
  
  return (
    <div style={styles.container}>
      <p style={styles.text}>Styled Box</p>
    </div>
  );
}
```

## CSS Modules

```css
/* Button.module.css */
.btn {
  background-color: blue;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn:hover {
  background-color: darkblue;
}
```

```javascript
// Button.js
import styles from './Button.module.css';

function Button() {
  return <button className={styles.btn}>Click me</button>;
}
```

## Tailwind CSS

```javascript
function Card() {
  return (
    <div className="bg-white rounded-lg shadow-lg p-6">
      <h2 className="text-2xl font-bold mb-4">Title</h2>
      <p className="text-gray-600">Description</p>
      <button className="mt-4 bg-blue-500 text-white px-4 py-2 rounded">
        Action
      </button>
    </div>
  );
}
```

---

**Next:** [05-api-integration.md](./05-api-integration.md)