# Tree Representation Of Lisp

I have a simple python script to turn lisp code into indented text.

```python
def lisp_to_indented_text(lisp_code):
    tokens = lisp_code.replace('(', ' ( ').replace(')', ' ) ').split()
    result = ""
    indent_level = 0
    begin = False

    for token in tokens:
        if token == '(':
            begin = True
            indent_level += 1
        elif token == ')':
            indent_level -= 1
        else:
            if begin:
                result += "\t" * (indent_level - 1) + token + "\n"
                begin = False
            else:
                result += "\t" * indent_level + token + "\n"

    return result
```

There are a lot of parenthesis in lisp. Each pair of parenthesis contains a list, and list can contain child lists. So it's already naturally a tree representation. But in the form of indented text, when there's a list, there's also always a header. So in this conversion, I just take the first element of each list as the header, and all other elements as the children.

For the following program in lisp (scheme):

```scheme
(define (fibonacci n)
	(if (<= n 1)
		n
		(+ (fibonacci (- n 1)) (fibonacci (- n 2)))))
```

The converted text looks like this:

```txt
define
	fibonacci
		n
	if
		<=
			n
			1
		n
		+
			fibonacci
				-
					n
					1
			fibonacci
				-
					n
					2
```

It's longer in lines, because each token takes one line, but it looks just as neat. Every method is the header, and the parameters are the children.

I think this format a more natural way to store code, as well as editing code. Code shouldn't necessarily be stored in pure text, but also in some binary way just as the AST, because the formatting of code isn't the essence, only the schema (AST) is. An editor could display it in any way the user wants, and allow user to modify the AST in place. And an interpreter could run it without parsing the text first.

One can also tweak this format of indented text a bit. For example, use invoke keyword for funtion calls, to make headers only contain keywords.

```txt
define
	fibonacci
		n
	if
		<=
			n
			1
		n
		+
			invoke
				fibonacci
				-
					n
					1
			invoke
				fibonacci
				-
					n
					2
```

Or, even more aggressively, one can write a program in json or other formats:

```json
{
	"name": "fibonacci",
	"parameters": [
		"n"
	],
	"body": [
		...
	]
}
```

But this feels a bit over-complicating in syntax and I couldn't complete it anymore.

I talked with ChatGPT about my ideas. [here](./ChatGPT-Binary%20Languages%20with%20Editors.md)
