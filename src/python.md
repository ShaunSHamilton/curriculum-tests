# Python

## Browser

```javascript,editable,mdbook-runnable,ignore,hidelines=#
# const __helpers = {
#  python: {
#    getDef: (code, functionName) => {
#      const regex = new RegExp(
#        `\\n(?<function_indentation> *?)def\\s+${functionName}\\s*\\((?<function_parameters>[^\\)]*)\\)\\s*:\\n(?<function_body>.*?)(?=\\n\\k<function_indentation>[\\w#]|$)`,
#       "s"
#      );
#
#      const matchedCode = regex.exec(code);
#      if (matchedCode) {
#        const { function_parameters, function_body, function_indentation } = matchedCode.groups;
#
#        const functionIndentationSansNewLine = function_indentation.replace(
#          /\n+/,
#          ""
#        );
#        return {
#          def: matchedCode[0],
#          function_parameters,
#          function_body,
#          function_indentation: functionIndentationSansNewLine.length,
#        };
#      }
#      return null;
#    }
#  }
# };
# const __pyodide = {
#  runPython: (code) => {
#    return code;
#  },
# };
const code = `
a = 1
b = 2

def add(x, y):
  result = x + y
  print(f"{x} + {y} = {result}")
  return result

`;

{
  const add = __helpers.python.getDef(code, "add");
  const { function_body, function_indentation, def, function_parameters } =
    add;
  const c = `
a = 100
b = 200

def add(${function_parameters}):
${' '.repeat(function_indentation)}assert ${function_parameters.split(',')[0]} == 100
${function_body}

assert add(a, b) == 300
`;
  const out = __pyodide.runPython(c); // If this does not throw, code is correct
  console.log(add);
}
```
