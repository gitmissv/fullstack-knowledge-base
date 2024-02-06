**All Schema Types**

>_required_: boolean or function, if true adds a [required validator](https://mongoosejs.com/docs/validation.html#built-in-validators) for this property
>
>_default_: Any or function, sets a default value for the path. If the value is a function, the return value of the function is used as the default.
>
>_select_: boolean, specifies default [projections](https://www.mongodb.com/docs/manual/tutorial/project-fields-from-query-results/) for queries
>
>_validate_: function, adds a [validator function](https://mongoosejs.com/docs/validation.html#built-in-validators) for this property
>
>_get_: function, defines a custom getter for this property using Object.defineProperty().
>
>_set_: function, defines a custom setter for this property using Object.defineProperty().
>
>_alias_: string, mongoose >= 4.10.0 only. Defines a virtual with the given name that gets/sets this path.
>
>_immutable_: boolean, defines path as immutable. Mongoose prevents you from changing immutable paths unless the parent document has isNew: true.
>
>_transform_: function, Mongoose calls this function when you call Document#toJSON() function, including when you JSON.stringify() a document.

**String**

>_lowercase_: boolean, whether to always call .toLowerCase() on the value
>
>_uppercase_: boolean, whether to always call .toUpperCase() on the value
>
>_trim_: boolean, whether to always call .trim() on the value
>
>_match_: RegExp, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value matches the given regular expression
>
>_enum_: Array, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is in the given array.
>
>_minLength_: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value length is not less than the given number
>
>_maxLength_: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value length is not greater than the given number
>
>_populate_: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)

**Number**

>_min_: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is greater than or equal to the given minimum.
>
>_max_: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is less than or equal to the given maximum.
>
>_enum_: Array, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is strictly equal to one of the values in the given array.
>
>_populate_: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)

**Date**

>_min_: Date, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is greater than or equal to the given minimum.
>
>_max_: Date, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is less than or equal to the given maximum.
>
>_expires_: Number or String, creates a TTL index with the value expressed in seconds.

**ObjectId**

>_populate_: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)