## Pipes
Pipes are features, build into Angular which allows to tranform output in the template.

For example, you have a property: `username = 'Max'`. You can use this property in your template:
`<p>{{ username }}</p>` It looks like `Max` on the screen. Now, you need to transform the property
to the upper case. You can use a pipe: `<p>{{ username | uppercase }}</p>`. Now it looks like `MAX`.
