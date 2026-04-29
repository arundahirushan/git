```
###COMMON MONGOOSE SCHEMA FIELDS (with meaning + examples)

name: {
  type: String,                    // Data type must be text
  required: [true, "Name is required"], // Cannot be empty
  trim: true,                      // Removes spaces before/after text
  minlength: [3, "Minimum 3 characters"], // At least 3 chars
  maxlength: [50, "Maximum 50 characters"], // Max 50 chars
},

email: {
  type: String,
  required: true,
  unique: true,                    // No duplicate values
  lowercase: true,                 // Converts to lowercase
  match: [/^\S+@\S+\.\S+$/, "Invalid email"], // Regex validation
},

price: {
  type: Number,
  required: true,
  min: [0, "Cannot be negative"], // Minimum value
  max: [100000, "Too expensive"], // Maximum value
},

stockQuantity: {
  type: Number,
  required: true,
  default: 0,                      // Default if not provided
  min: 0,
},

category: {
  type: String,
  enum: ["Electronics", "Clothing", "Food"], // Only these values allowed
},

isAvailable: {
  type: Boolean,                   // true / false
  default: true,
},

createdAt: {
  type: Date,                      // Stores date/time
  default: Date.now,
},

tags: [{
  type: String                     // Array of strings
}],

userId: {
  type: mongoose.Schema.Types.ObjectId, // Reference to another collection
  ref: "User",
},

imageUrl: {
  type: String,
  default: "",
},

password: {
  type: String,
  required: true,
  select: false,                   // Hidden by default in queries
},
```
```

## Most Commonly Used Options Explained

### `type`

Defines what kind of data is stored.

```javascript
type: String
type: Number
type: Boolean
type: Date
type: Array
type: ObjectId
```

---

### `required`

Makes the field mandatory.

```javascript
required: true
required: [true, "Custom error message"]
```

---

### `default`

Automatically sets a value if none is provided.

```javascript
default: 0
default: ""
default: Date.now
```

---

### `trim`

Removes extra spaces.

```javascript
"  Laptop  " → "Laptop"
```

---

### `unique`

Prevents duplicates.

```javascript
email must be different for every user
```

---

### `min` / `max`

Used mostly for numbers.

```javascript
age: { type: Number, min: 18, max: 60 }
```

---

### `minlength` / `maxlength`

Used for strings.

```javascript
username: { minlength: 4, maxlength: 20 }
```

---

### `enum`

Restricts allowed values.

```javascript
status: {
  type: String,
  enum: ["Pending", "Completed", "Cancelled"]
}
```

---

### `match`

Regex validation.

```javascript
match: [/^\d{10}$/, "Phone must be 10 digits"]
```

---

### `lowercase` / `uppercase`

Automatically changes text case.

```javascript
lowercase: true
```

---

### `select`

Hide sensitive fields by default.

```javascript
password: {
  type: String,
  select: false
}
```

---

# Real MERN Item Example:

```javascript
const itemSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    trim: true
  },
  category: {
    type: String,
    required: true,
    enum: ["Electronics", "Furniture", "Food"]
  },
  price: {
    type: Number,
    required: true,
    min: 0
  },
  stockQuantity: {
    type: Number,
    required: true,
    min: 0,
    default: 0
  },
  isAvailable: {
    type: Boolean,
    default: true
  }
}, { timestamps: true });
```

## Pro Tip for exams:

### Most commonly used:

* `type`
* `required`
* `default`
* `trim`
* `unique`
* `min`
* `max`
* `enum`

These cover most CRUD applications.
