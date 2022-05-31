# Problems in Vscode & Python

 

- Problem: Cannot activate the 'Python' extension because it depends on the 'jupyter' extension, which is not loaded.

  ​	- Solve: **Uninstalled Jupyter, pylance, and python extensions in vscode. then re-installed and everything started working again**







## Vscode 的颜色设置

https://code.visualstudio.com/api/references/theme-color#minimap



可以设置minimap的颜色细节。





```json
"workbench.colorCustomizations": {

        "minimapSlider.hoverBackground": "#a4a4a483",
        "minimapSlider.background": "#a4a4a45c",
        // "minimap.findMatchHighlight": "#ff0000",
        "minimap.selectionHighlight": "#ffffff",
        "minimap.selectionOccurrenceHighlight": "#ffffff"
  
```
