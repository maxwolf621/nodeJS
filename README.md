# nodeJS Joi

Joi provides various other methods for defining validation rules, such as `.string()`, `.number()`, `.array()`, and more. 

## Structure creation

Create a base schema for an object (define the strcture of an object)  
```typescript
Joi.object()
```

For example defining an object with keys `field_a` (a number between 1 and 10) and `field_b` (any value)  
```typescript
const schema = Joi.object({  
  field_a : Joi.number().min(1).max(10).integer(),
  field_b : Joi.any(),
});
```

## DINAMICALLY add validations

```typescript
Joi.object().keys()
```

If you're writing your schema once, you don't necessarily need to use `Joi.object().keys()`.   
- `Joi.object()` directly is sufficient.

However, `Joi.object().keys()` becomes more useful when you want to add more keys DYNAMICALLY (e.g., calling .keys() multiple times). 

```typescript  
const blogPostSchema = Joi.object().keys({ 
  title: Joi.string().alphanum().min(3).max(30).required(),
  description: Joi.string(), 
  comments: Joi.array().items(Joi.object.keys({ 
    description: Joi.string(), 
    author: Joi.string().required(), 
    grade: Joi.number().min(1).max(5) 
  })) 
});
```

> It's a way to make your code more explicit and maintainable.  

## Validate


---

References
- https://softchris.github.io/pages/joi.html#introducing-joi
