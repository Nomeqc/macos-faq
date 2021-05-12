
## 下载辅助库
1. Download the alfred-workflow-X.X.X.zip from the [GitHub releases page](https://github.com/deanishe/alfred-workflow/releases).
2. Extract the ZIP archive and place the workflow directory in the root folder of your workflow (where info.plist is).

## 示例：
```py
#!/usr/bin/python
# encoding: utf-8

import sys

# Workflow3 supports Alfred 3's new features. The `Workflow` class
# is also compatible with Alfred 2.
from workflow import Workflow3, web, ICON_INFO, ICON_ERROR


def get_short_text(code=''):
    url = 'https://tools.201992.xyz/s/query.php?short_code={}'.format(code)
    resp = web.get(url)
    resp.raise_for_status()
    result = resp.json()
    return result.get('text'), result.get('error')

def main(wf):
    param = (wf.args[0] if len(wf.args) else '').strip()
    if not param:
        return
    text, error = get_short_text(code=param)
    if not error:
        wf.add_item(title=text, subtitle='选择复制到剪贴板', arg=text, valid=True, icon=ICON_INFO)
    else:
        wf.add_item(title=error, subtitle='...', icon=ICON_ERROR)
    wf.send_feedback()


if __name__ == '__main__':
    # Create a global `Workflow3` object
    wf = Workflow3()
    # Call your entry function via `Workflow3.run()` to enable its
    # helper functions, like exception catching, ARGV normalization,
    # magic arguments etc.
    sys.exit(wf.run(main))
```
