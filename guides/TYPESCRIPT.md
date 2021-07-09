# TypeScript

## Avoid casting unless absolutely necessary

It makes code harder to understand, less predictable, and less dependable. It
also forces the next developer to verify that the cast isn't breaking anything.
What if you do something like `x as User`, but the type of `x` isn't actually
`User` for some reason?

## Avoid using "any"

If you really don't know what a thing is, use "unknown" instead.
