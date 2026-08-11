# chatgpt2dlg

Convert a ChatGPT conversation into an [aidialog](https://github.com/AnswerDotAI/aidialog) dialog you can read, search, and edit.

## Install

    pip install chatgpt2dlg

## Use

`convo2dlg` turns a conversation payload, the JSON ChatGPT's web app loads, into a dialog:

    from chatgpt2dlg import convo2dlg
    convo2dlg(payload).save('chat.ipynb')

Fetching the payload needs a logged-in browser, because ChatGPT won't serve it to a plain HTTP client. The easiest way is `url2convo` with [fastcdp](https://github.com/AnswerDotAI/fastcdp), which fetches through a browser tab that already holds your login:

    from fastcdp.skill import ExtCDP
    from chatgpt2dlg import url2convo, convo2dlg
    cdp  = await ExtCDP.listen()
    page = await cdp.new_page()
    convo2dlg(await url2convo('https://chatgpt.com/c/<id>', page)).save('chat.ipynb')

Point it at a conversation you can open: your own while logged in, or a Share link. For other ways to get the payload, see `nbs/00_core.ipynb`.
