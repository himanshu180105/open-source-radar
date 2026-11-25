# 2. अपने टूल सेट अप करें

आपको Git, एक GitHub अकाउंट, authenticate करने का एक तरीका, एक editor, और आप जो प्रोजेक्ट चुनते हैं उसकी भाषा का toolchain चाहिए होगा। इसे एक बार सेट अप करने में लगभग एक घंटा लगता है।

## Git

Git इंस्टॉल करें:

- **macOS:** `xcode-select --install` (Command Line Tools के साथ Git इंस्टॉल करता है), या [Homebrew](https://brew.sh) के साथ `brew install git`।
- **Windows:** [Git for Windows](https://git-scm.com/download/win)। इसमें Git Bash शामिल होता है, जो एक terminal है और इस गाइड में दिए गए commands को चलाता है।
- **Linux:** आपका package manager, उदाहरण के लिए `sudo apt install git` या `sudo dnf install git`।

Git को बताएँ कि आप कौन हैं। अपने GitHub अकाउंट वाला ही ईमेल इस्तेमाल करें (या GitHub का प्राइवेट noreply पता इस्तेमाल करें, नीचे देखें) ताकि आपके commits आपकी प्रोफ़ाइल से जुड़ सकें:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase true
```

### अपना ईमेल प्राइवेट रखें (वैकल्पिक)

GitHub हर अकाउंट को `12345678+username@users.noreply.github.com` जैसा एक noreply पता देता है। **Settings → Emails** में जाकर अपना पता देखें, **Keep my email addresses private** को चालू करें, और उस पते को `user.email` के रूप में इस्तेमाल करें। इसके बाद भी commits आपकी प्रोफ़ाइल पर गिने जाएँगे।

> **आम गलती:** ऐसे ईमेल से commit करना जो आपके GitHub अकाउंट में जुड़ा न हो। ऐसे commits बिना आपके avatar के दिखते हैं और आपकी प्रोफ़ाइल पर नहीं गिने जाते। `git config user.email` चलाकर जाँचें और **Settings → Emails** से मिलान करें।

## GitHub अकाउंट और authentication

1. [github.com](https://github.com) पर एक अकाउंट बनाएँ। एक पेशेवर username चुनें; यह आपके हर योगदान पर दिखाई देता है।
2. **Settings → Password and authentication** में जाकर two-factor authentication चालू करें। कई संगठन इसे ज़रूरी मानते हैं।
3. Git के लिए authenticate करने का एक तरीका सेट अप करें। सबसे आसान तरीका GitHub CLI है:

```bash
# macOS: brew install gh   Windows: winget install GitHub.cli   Linux: see cli.github.com
gh auth login          # choose GitHub.com, HTTPS, and log in with a browser
gh auth setup-git      # lets git push over HTTPS using that login
```

इसके अलावा, आप [एक SSH key जोड़ सकते हैं](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) और `git@github.com:` URLs के साथ clone कर सकते हैं।

## एक editor

जिसमें आप सहज हों उसका इस्तेमाल करें। [VS Code](https://code.visualstudio.com) एक आम पसंद है: इसमें अच्छा Git integration है, और इसके आधिकारिक language extensions आपको formatting और error checking की सुविधा देते हैं। JetBrains IDEs, Neovim, Zed और Emacs भी सभी बढ़िया विकल्प हैं।

दो settings आपको review comments से बचाती हैं:

- प्रोजेक्ट के formatter (Prettier, Black, rustfmt, gofmt आदि) के साथ **Format on save**।
- **`.editorconfig` का पालन करें**। कई प्रोजेक्ट indentation और line endings सेट करने के लिए यह फ़ाइल साथ रखते हैं।

## वे Git commands जिनका आप वास्तव में उपयोग करेंगे

| Command | यह क्या करता है |
| --- | --- |
| `git clone URL` | किसी repository को डाउनलोड करना |
| `git status` | यह देखना कि क्या बदला है |
| `git switch -c fix-typo` | एक नई branch बनाना और उस पर स्विच करना |
| `git add path/to/file` | अगले commit के लिए किसी बदलाव को stage करना |
| `git commit -m "message"` | stage किए गए बदलावों को रिकॉर्ड करना |
| `git push -u origin fix-typo` | अपनी branch को अपलोड करना |
| `git fetch upstream` | मूल प्रोजेक्ट से नवीनतम बदलाव डाउनलोड करना |
| `git rebase upstream/main` | उन बदलावों के ऊपर अपने commits को फिर से लागू करना |
| `git log --oneline -10` | हाल के commits देखना |
| `git diff` | unstage किए गए बदलाव देखना (stage किए गए बदलावों के लिए `git diff --staged`) |

अगर आपने पहले कभी Git का उपयोग नहीं किया है, तो पहले 30 मिनट [Learn Git Branching](https://learngitbranching.js.org) पर बिताएँ। यह interactive है और ठीक वही सिखाता है जिसकी आपको ज़रूरत है।

## भाषा के toolchains

आप जो प्रोजेक्ट चुनते हैं उसके लिए toolchain इंस्टॉल करें, और वही वर्ज़न इस्तेमाल करें जो प्रोजेक्ट माँगता है (`.nvmrc`, `.python-version`, `rust-toolchain.toml`, `go.mod`, `.tool-versions` जैसी फ़ाइलें देखें)। [language quickstarts](../../languages/README.md) में हर भाषा के सामान्य commands की सूची दी गई है।

Version managers इसे आसान बना देते हैं:

- **कई भाषाएँ:** [mise](https://mise.jdx.dev) या [asdf](https://asdf-vm.com)
- **Node.js:** [fnm](https://github.com/Schniz/fnm) या nvm, साथ ही pnpm और Yarn के लिए `corepack enable`
- **Python:** [uv](https://docs.astral.sh/uv/) (`uv python install 3.12`)
- **Rust:** [rustup](https://rustup.rs)
- **Go:** आधिकारिक installer, या आपका package manager; जब `go.mod` नए toolchain की माँग करता है, तो Go उसे खुद डाउनलोड कर लेता है

## चेकलिस्ट

- [ ] `git --version` काम करता है और `git config user.email` मेरे GitHub अकाउंट के किसी ईमेल से मेल खाता है।
- [ ] Two-factor authentication चालू है।
- [ ] `gh auth status` (या `ssh -T git@github.com`) दिखाता है कि मैं authenticate कर सकता/सकती हूँ।
- [ ] मेरा editor save करने पर format करता है।

अगला: [एक प्रोजेक्ट चुनें](03-choose-a-project.md)
