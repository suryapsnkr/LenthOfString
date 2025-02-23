# LenthOfString
<!doctype html>
<html lang="en">

<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>PyScript Example</title>
  <link rel="stylesheet" href="https://pyscript.net/releases/2024.1.1/core.css" />
  <script type="module" src="https://pyscript.net/releases/2024.1.1/core.js"></script>
</head>

<body>
  <center>
    <h1>PyScript Text Length Counter</h1>
    <textarea id="input_text" placeholder="Enter Your Text"></textarea><br><br>

    <button id="run" type="button">Count</button>
    <button id="clear" type="button">Clear</button><br><br>

    <p id="output"></p>
  </center>

  <script type="py" id="pyscript">
    from js import document
    from pyodide.ffi import create_proxy  # ✅ Import create_proxy to prevent errors

    def clear(event):
        document.getElementById("input_text").value = ""
        document.getElementById("output").innerText = ""

    def count(event):
        text_value = document.getElementById("input_text").value
        text_length = len(text_value)
        document.getElementById("output").innerText = f"Length of String is: {text_length}"

    # ✅ Create proxies to avoid garbage collection issues
    count_proxy = create_proxy(count)
    clear_proxy = create_proxy(clear)

    # ✅ Attach event listeners using the proxies
    document.getElementById("run").addEventListener("click", count_proxy)
    document.getElementById("clear").addEventListener("click", clear_proxy)
  </script>
</body>

</html>
