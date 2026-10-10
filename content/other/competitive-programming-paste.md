# Competitive Programming Paste

This is a userscript that makes it easy to create a directory, test files, and the program template for problems on Kattis, CSES, and Codeforces. Use it with [cptest](./cptest.md).

It adds a button by the problem title:

![](/assets/cppaste.png)

Copying it adds Bash or PowerShell (configurable) code to your clipboard:

```bash
 { d=$PWD; cur=${d##*/}; par=${d%/*}; par=${par##*/}; if grep -iqE '(kattis|cses|codeforces|20[0-9]*)' <<< "$cur"; then :; elif grep -iqE '(kattis|cses|codeforces|20[0-9]*)' <<< "$par"; then cd ..; else echo "Error: Not in a problem directory" >&2; false; fi && { if [[ -d 'romans' ]]; then echo "Directory already exists: romans" >&2; else mkdir -p 'romans'; cat > 'romans/romans.cpp' <<< $'#include <bits/stdc++.h>\n#define ISDEBUG\n#ifdef ISDEBUG\n   #define debug(s) cout << s << endl\n   #define vdebug(s) debug(#s << ": " << s)\n#else\n   #define debug(s)\n   #define vdebug(s)\n#endif\nusing namespace std;\nnamespace rg = ranges;\nusing ll = long long;\nusing pri = pair<int, int>;\nusing prl = pair<ll, ll>;\nusing vi = vector<int>;\nusing vll = vector<ll>;\n#define loop(i, a, b) for (int i = a; i < (b); ++i)\n#define loopt(i, a, b, T) for (T i = a; i < (b); ++i)\n#define say(s) cout << s << endl\n#define be(x) (x).begin(), (x).end()\ntemplate <typename T> static T read() {\n   T x; cin >> x; return x;\n}\ntemplate <typename T> static ostream &operator<<(ostream &os, const vector<T> &v) {\n   os << \'[\';\n   for (auto i = 0; i < v.size(); ++i) {\n      os << v[i];\n      if (i + 1 < v.size()) os << ", ";\n   }\n   os << \']\';\n   return os;\n}\ntemplate <class K, class V> static ostream &operator<<(ostream &os, const map<K, V> &m) {\n   os << \'{\';\n   for (auto it = m.begin(); it != m.end(); ++it) {\n      os << it->first << ": " << it->second;\n      if (std::next(it) != m.end()) os << ", ";\n   }\n   os << \'}\';\n   return os;\n}\n\nint main() {\n   cin.tie(nullptr)->sync_with_stdio(false);\n   // cin.exceptions(cin.failbit);\n}\n'; cat > 'romans/in1' <<< $'1.0'; cat > 'romans/out1' <<< $'1088'; cat > 'romans/in2' <<< $'20.267'; cat > 'romans/out2' <<< $'22046'; cd 'romans'; fi; }; }
```

Pasting it in the terminal creates files with the right contents:

```
$ tree --noreport romans/
romans/
├── in1
├── in2
├── out1
├── out2
└── romans.cpp
```

This code lies in a userscript. First, install [ViolentMonkey](https://violentmonkey.github.io/). Then, add the code below.

This code allows for configuring quite a few things via a settings menu. Usually, you can see it if you click the ViolentMonkey icon in the browser toolbar. You'll only see it if you're on the right Kattis etc. page.

```javascript
// ==UserScript==
// @name         Competitive Programming Paste
// @namespace    com.edwinkofler
// @author       Edwin Kofler
// @description  Create setup files for competitive programming problems for various websites.
// @version      1.3.0
// @match        https://open.kattis.com/problems/*
// @match        https://open.kattis.com/challenge/*
// @match        https://open.kattis.com/contests/*
// @match        https://cses.fi/problemset/task/*
// @match        https://codeforces.com/contest/*/problem/*
// @match        https://codeforces.com/problemset/problem/*/*
// @match        https://codeforces.com/gym/*/problem/*
// @grant        GM_setClipboard
// @grant        GM_registerMenuCommand
// @grant        GM_getValue
// @grant        GM_setValue
// @run-at       document-end
// @require      https://raw.githubusercontent.com/hyperupcall-projects/GM_config/v0.1.0/gm_config.js
// @icon         data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxZW0iIGhlaWdodD0iMWVtIiB2aWV3Qm94PSIwIDAgNTEyIDUxMiI+Cgk8cGF0aCBkPSJNMCAwaDUxMnY1MTJIMHoiIGZpbGw9Im5vbmUiIC8+Cgk8cGF0aCBmaWxsPSIjRDE5QjYxIiBkPSJNNDAyLjYzNCA1MDUuNjg3SDEwOS4zNjZjLTE5Ljg4MiAwLTM2LTE2LjExOC0zNi0zNlY5My44MjJjMC0xOS44ODIgMTYuMTE4LTM2IDM2LTM2aDI5My4yNjdjMTkuODgyIDAgMzYgMTYuMTE4IDM2IDM2djM3NS44NjRjLjAwMSAxOS44ODMtMTYuMTE3IDM2LjAwMS0zNS45OTkgMzYuMDAxIiAvPgoJPHBhdGggZmlsbD0iI0Y5RjlGNyIgZD0iTTM4Ni4xNTIgNDYzLjY3M0gxMjUuODQ4Yy03Ljk1MyAwLTE0LjQtNi40NDctMTQuNC0xNC40VjEwMi4zMDZjMC03Ljk1MyA2LjQ0Ny0xNC40IDE0LjQtMTQuNGgyNjAuMzA1YzcuOTUzIDAgMTQuNCA2LjQ0NyAxNC40IDE0LjR2MzQ2Ljk2N2MtLjAwMSA3Ljk1My02LjQ0OCAxNC40LTE0LjQwMSAxNC40IiAvPgoJPHBhdGggZmlsbD0iI0E5QjhDMiIgZD0iTTM0MC4wMjcgMjAwLjMwNkgxNTMuNTA4YTcuNzcyIDcuNzcyIDAgMSAxIDAtMTUuNTQ0aDE4Ni41MTlhNy43NzIgNy43NzIgMCAxIDEgMCAxNS41NDRtLTc2LjI1NSAzNi4wNjVhNy43NyA3Ljc3IDAgMCAwLTcuNzcyLTcuNzcySDE1My41MDhhNy43NzIgNy43NzIgMCAxIDAgMCAxNS41NDRIMjU2YTcuNzcgNy43NyAwIDAgMCA3Ljc3Mi03Ljc3Mm0wLTg4LjAxNmE3Ljc3IDcuNzcgMCAwIDAtNy43NzItNy43NzJIMTUzLjUwOGE3Ljc3MiA3Ljc3MiAwIDEgMCAwIDE1LjU0NEgyNTZhNy43NyA3Ljc3IDAgMCAwIDcuNzcyLTcuNzcyTTM0Ny44IDI4MC4yMDhhNy43NyA3Ljc3IDAgMCAwLTcuNzcyLTcuNzcyaC0xODYuNTJhNy43NzIgNy43NzIgMCAwIDAgMCAxNS41NDRoMTg2LjUxOWE3Ljc3MyA3Ljc3MyAwIDAgMCA3Ljc3My03Ljc3Mm0tNTUuOTU2IDQzLjgzOGE3Ljc3IDcuNzcgMCAwIDAtNy43NzItNy43NzJIMTUzLjUwOGE3Ljc3MiA3Ljc3MiAwIDAgMCAwIDE1LjU0NGgxMzAuNTYzYTcuNzczIDcuNzczIDAgMCAwIDcuNzczLTcuNzcybTU1Ljk1NiA0My44MzdhNy43NyA3Ljc3IDAgMCAwLTcuNzcyLTcuNzcyaC0xODYuNTJhNy43NzIgNy43NzIgMCAwIDAgMCAxNS41NDRoMTg2LjUxOWE3Ljc3MyA3Ljc3MyAwIDAgMCA3Ljc3My03Ljc3Mk0yMjYuNTYyIDQxMS43MmE3Ljc3IDcuNzcgMCAwIDAtNy43NzItNy43NzJoLTY1LjI4MmE3Ljc3MiA3Ljc3MiAwIDAgMCAwIDE1LjU0NGg2NS4yODJhNy43NyA3Ljc3IDAgMCAwIDcuNzcyLTcuNzcyIiAvPgoJPHBhdGggZmlsbD0iI0I5QzVDNiIgZD0iTTMwNy4wNDIgMzUuNjU0aC0xNS4zODhDMjkxLjY1NCAxNS45NjMgMjc1LjY5MSAwIDI1NiAwcy0zNS42NTQgMTUuOTYzLTM1LjY1NCAzNS42NTRoLTE1LjM4OGMtMTkuODgyIDAtMzYgMTYuMTE4LTM2IDM2djM2Ljk4YTcuMiA3LjIgMCAwIDAgNy4yIDcuMmgxNTkuNjg1YTcuMiA3LjIgMCAwIDAgNy4yLTcuMnYtMzYuOThjLS4wMDEtMTkuODgyLTE2LjExOC0zNi0zNi4wMDEtMzYiIC8+Cgk8Y2lyY2xlIGN4PSIyNTYiIGN5PSIzNS42NTQiIHI9IjIzLjQxIiBmaWxsPSIjMkIzQjQ3IiAvPgo8L3N2Zz4K
// ==/UserScript==

(function () {
	"use strict";

	const SITE = location.hostname.includes("cses.fi")
		? "cses"
		: location.hostname.includes("codeforces.com")
			? "codeforces"
			: location.hostname.includes("kattis.com")
				? "kattis"
				: null;
	if (!SITE) return;

	/** @returns {{ dirName: string, sourceBase: string, javaClass: string, titleEl: HTMLElement | null } | null} */
	function getProblemInfo() {
		if (SITE === "kattis") {
			const isChallenge = location.pathname.includes("/challenge/");
			const slug = isChallenge
				? "_challenge"
				: location.pathname.split("/problems/")[1]?.split("/")[0];
			if (!slug) return null;
			return {
				dirName: slug,
				sourceBase: slug,
				javaClass: slug,
				titleEl: document.querySelector("h1.book-page-heading"),
			};
		}

		if (SITE === "cses") {
			const taskMatch = location.pathname.match(/\/problemset\/task\/(\d+)/);
			const titleEl = document.querySelector(".title-block h1");
			if (!taskMatch || !titleEl) return null;
			return {
				dirName: titleEl.textContent.trim(),
				sourceBase: "main",
				javaClass: "Main",
				titleEl,
			};
		}

		const titleEl = document.querySelector(".problem-statement .header .title");
		if (!titleEl) return null;
		const title = titleEl.textContent.trim();
		return {
			dirName: title.replace(/^[A-Za-z0-9]+\.\s*/, ""),
			sourceBase: "main",
			javaClass: "Main",
			titleEl,
		};
	}

	const problem = getProblemInfo();
	if (!problem?.titleEl) return;

	const { dirName, sourceBase, javaClass, titleEl } = problem;

	const gmcfg = new GM_config({
		id: "CompetitivePasteConfig",
		title: "Competitive Paste Settings",
		css: [
			"#CompetitivePasteConfig { font-family: system-ui, sans-serif; line-height: 1.4; }",
			"#CompetitivePasteConfig .config_header { font-size: 1.25rem; margin-bottom: 1rem; }",
			"#CompetitivePasteConfig .config_var { margin-bottom: 0.85rem; }",
			"#CompetitivePasteConfig .field_label { display: block; font-size: 0.85rem; margin-bottom: 0.25rem; }",
			"#CompetitivePasteConfig input[type=text], #CompetitivePasteConfig select { max-width: 24rem; width: 100%; padding: 0.25rem 0.4rem; }",
			"#CompetitivePasteConfig textarea { width: 100%; min-height: 5.5rem; font-family: ui-monospace, monospace; font-size: 0.8rem; padding: 0.4rem; box-sizing: border-box; }",
			"#CompetitivePasteConfig .saveclose_buttons { margin-top: 1rem; padding: 0.35rem 0.75rem; }",
			"#CompetitivePasteConfig .section_desc { text-align: left; font-size: 0.8rem; padding: 0.4rem 0.5rem; border-radius: 4px; }",
		].join("\n"),
		fields: {
			language: {
				label: "Language",
				type: "select",
				options: ["C++", "Java", "Python"],
				default: "C++",
			},
			shell: {
				label: "Shell",
				type: "select",
				options: ["Bash or Zsh", "PowerShell Core"],
				default: "Bash or Zsh",
			},
			inputFilename: {
				label: "Input filename pattern for test cases (use {n} for number)",
				type: "text",
				default: "in{n}",
			},
			outputFilename: {
				label: "Output filename pattern for test cases (use {n} for number)",
				type: "text",
				default: "out{n}",
			},
			problemDirRegex: {
				label: "Problem directory regex (case-insensitive)",
				type: "text",
				default: "(kattis|cses|codeforces|20[0-9]*)",
				section: [
					"",
					'For the regex below, Bash/Zsh uses <a href="https://www.gnu.org/software/grep/manual/html_node/Regular-Expressions.html" target="_blank" rel="noopener noreferrer">POSIX extended regexes)</a> and PowerShell uses <a href="https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference" target="_blank" rel="noopener noreferrer">.NET regexes</a>.',
				],
			},
			cppTemplate: {
				label: "C++ default template",
				type: "textarea",
				default: `#include <bits/stdc++.h>
using namespace std;

int main() {

}`,
			},
			javaTemplate: {
				label: "Java default template (use {class} for the class name)",
				type: "textarea",
				default: `import java.util.*;

public class {class} {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

    }
}`,
			},
			pythonTemplate: {
				label: "Python default template",
				type: "textarea",
				default: `import sys
`,
			},
		},
	});

	GM_registerMenuCommand("Settings/Preferences", () => gmcfg.open());

	function getLanguageConfig() {
		return {
			"C++": {
				ext: "cpp",
				template: gmcfg.get("cppTemplate"),
			},
			Java: {
				ext: "java",
				template: gmcfg.get("javaTemplate").replaceAll("{class}", javaClass),
			},
			Python: {
				ext: "py",
				template: gmcfg.get("pythonTemplate"),
			},
		};
	}

	function getKattisSamples() {
		const samples = [];
		const tables = document.querySelectorAll("table.sample");

		for (let i = 0; i < tables.length; i++) {
			/** @type {HTMLTableElement} */
			const table = tables[i];
			const cells = table.querySelectorAll("td");
			if (cells.length >= 2) {
				const inputPre = cells[0].querySelector("pre");
				const outputPre = cells[1].querySelector("pre");
				samples.push({
					input: inputPre ? inputPre.innerText : "",
					output: outputPre ? outputPre.innerText : "",
				});
			}
		}

		if (samples.length === 0) {
			const inputEls = document.querySelectorAll(
				".sampleinput pre, .sampledata pre",
			);
			const inputTexts = [];
			const outputTexts = [];
			for (let i = 0; i < inputEls.length; i++) {
				/** @type {HTMLPreElement} */
				const pre = inputEls[i];
				if (i % 2 === 0) inputTexts.push(pre.innerText);
				else outputTexts.push(pre.innerText);
			}
			for (let i = 0; i < inputTexts.length; i++) {
				samples.push({
					input: inputTexts[i],
					output: outputTexts[i] || "",
				});
			}
		}

		return samples;
	}

	function getCsesSamples() {
		const samples = [];
		const headings = document.querySelectorAll(".md h1");
		/** @type {HTMLElement | null} */
		let exampleHeading = null;

		for (const heading of headings) {
			if (/^example/i.test(heading.textContent.trim())) {
				exampleHeading = heading;
				break;
			}
		}
		if (!exampleHeading) return samples;

		let el = exampleHeading.nextElementSibling;
		while (el && el.tagName !== "H1") {
			if (el.tagName === "P" && /^Input:/i.test(el.textContent.trim())) {
				const inputPre = el.nextElementSibling;
				if (inputPre?.tagName === "PRE") {
					let out = inputPre.nextElementSibling;
					while (
						out &&
						out.tagName === "P" &&
						!/^Output:/i.test(out.textContent.trim())
					) {
						out = out.nextElementSibling;
					}
					if (out?.tagName === "P" && /^Output:/i.test(out.textContent.trim())) {
						const outputPre = out.nextElementSibling;
						if (outputPre?.tagName === "PRE") {
							samples.push({
								input: inputPre.innerText,
								output: outputPre.innerText,
							});
						}
					}
				}
			}
			el = el.nextElementSibling;
		}

		return samples;
	}

	function getCodeforcesSamples() {
		const samples = [];
		for (const test of document.querySelectorAll(".sample-test")) {
			const inputPre = test.querySelector(".input pre");
			const outputPre = test.querySelector(".output pre");
			if (inputPre && outputPre) {
				samples.push({
					input: inputPre.innerText,
					output: outputPre.innerText,
				});
			}
		}
		return samples;
	}

	function getSamples() {
		if (SITE === "cses") return getCsesSamples();
		if (SITE === "codeforces") return getCodeforcesSamples();
		return getKattisSamples();
	}

	function quoteBashSingle(/** @type {string} */ value) {
		return `'${value.replace(/'/g, "'\\''")}'`;
	}

	function quotePowerShellSingle(/** @type {string} */ value) {
		return `'${value.replace(/'/g, "''")}'`;
	}

	function buildScript(
		/** @type {Array<{input: string, output: string}>} */ samples,
	) {
		const langConfig = getLanguageConfig()[gmcfg.get("language")];
		/** @type {string} */
		const ext = langConfig.ext;
		/** @type {string} */
		const template = langConfig.template;
		const sourceFile = `${sourceBase}.${ext}`;
		const dirQuotedBash = quoteBashSingle(dirName);
		const sourcePathBash = quoteBashSingle(`${dirName}/${sourceFile}`);
		const dirQuotedPs = quotePowerShellSingle(dirName);
		const sourcePathPs = quotePowerShellSingle(`${dirName}/${sourceFile}`);

		const dirExistsMsg = dirName.replace(/'/g, "''");
		const dirExistsMsgBash = dirName.replace(/'/g, "'\\''");
		const problemDirRegex = gmcfg.get("problemDirRegex");
		const regexQuotedBash = quoteBashSingle(problemDirRegex);
		const regexQuotedPs = quotePowerShellSingle(problemDirRegex);

		if (gmcfg.get("shell") === "PowerShell Core") {
			const templateEscaped = template.replace(/\n/g, "\\n").replace(
				/'/g,
				"''",
			);

			const dirCheckPs =
				`$cur = Split-Path -Leaf (Get-Location); $par = Split-Path -Leaf (Split-Path -Parent (Get-Location)); if ($cur -match ${regexQuotedPs}) { } elseif ($par -match ${regexQuotedPs}) { cd .. } else { [Console]::Error.WriteLine("Error: Not in a problem directory"); return }; `;

			let script =
				` & { ${dirCheckPs}if (Test-Path ${dirQuotedPs}) { [Console]::Error.WriteLine("Directory already exists: ${dirExistsMsg}"); return } else { `;

			script +=
				`New-Item -ItemType Directory -Path ${dirQuotedPs} | Out-Null; '${templateEscaped}' -replace '\\n', "\`n" | Out-File -FilePath ${sourcePathPs} -Encoding utf8; `;

			for (let i = 0; i < samples.length; i++) {
				/** @type {{input: string, output: string}} */
				const s = samples[i];
				const n = i + 1;
				const inputContent = s.input.replace(/\n$/, "").replace(/\n/g, "\\n")
					.replace(/'/g, "''");
				const outputContent = s.output.replace(/\n$/, "").replace(/\n/g, "\\n")
					.replace(/'/g, "''");
				const inFile = gmcfg.get("inputFilename").replaceAll("{n}", n);
				const outFile = gmcfg.get("outputFilename").replaceAll("{n}", n);
				const inPathPs = quotePowerShellSingle(`${dirName}/${inFile}`);
				const outPathPs = quotePowerShellSingle(`${dirName}/${outFile}`);
				script +=
					`'${inputContent}' -replace '\\n', "\`n" | Out-File -FilePath ${inPathPs} -Encoding utf8; `;
				script +=
					`'${outputContent}' -replace '\\n', "\`n" | Out-File -FilePath ${outPathPs} -Encoding utf8; `;
			}
			script += `cd ${dirQuotedPs}; } }`;

			return script;
		}

		const dirCheckBash =
			` d=\$PWD; cur=\${d##*/}; par=\${d%/*}; par=\${par##*/}; if grep -iqE ${regexQuotedBash} <<< "\$cur"; then :; elif grep -iqE ${regexQuotedBash} <<< "\$par"; then cd ..; else echo "Error: Not in a problem directory" >&2; false; fi && { `;

		let script =
			` {${dirCheckBash}if [[ -d ${dirQuotedBash} ]]; then echo "Directory already exists: ${dirExistsMsgBash}" >&2; else `;

		const templateEscaped = template.replace(/\n/g, "\\n").replace(
			/'/g,
			"\\'",
		);
		script +=
			`mkdir -p ${dirQuotedBash}; cat > ${sourcePathBash} <<< $'${templateEscaped}'; `;

		for (let i = 0; i < samples.length; i++) {
			/** @type {{input: string, output: string}} */
			const s = samples[i];
			const n = i + 1;
			const inputContent = s.input.replace(/\n$/, "").replace(/\n/g, "\\n")
				.replace(/'/g, "\\'");
			const outputContent = s.output.replace(/\n$/, "").replace(/\n/g, "\\n")
				.replace(/'/g, "\\'");
			const inFile = gmcfg.get("inputFilename").replaceAll("{n}", n);
			const outFile = gmcfg.get("outputFilename").replaceAll("{n}", n);
			script += `cat > ${quoteBashSingle(`${dirName}/${inFile}`)} <<< $'${inputContent}'; `;
			script += `cat > ${quoteBashSingle(`${dirName}/${outFile}`)} <<< $'${outputContent}'; `;
		}
		script += `cd ${dirQuotedBash}; fi; }; }`;

		return script;
	}

	if (titleEl.querySelector(".competitive-paste-copy")) return;

	const COPY_ICON =
		'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 640" aria-hidden="true"><path d="M360 160L280 160C266.7 160 256 149.3 256 136C256 122.7 266.7 112 280 112L360 112C373.3 112 384 122.7 384 136C384 149.3 373.3 160 360 160zM360 208C397.1 208 427.6 180 431.6 144L448 144C456.8 144 464 151.2 464 160L464 512C464 520.8 456.8 528 448 528L192 528C183.2 528 176 520.8 176 512L176 160C176 151.2 183.2 144 192 144L208.4 144C212.4 180 242.9 208 280 208L360 208zM419.9 96C407 76.7 385 64 360 64L280 64C255 64 233 76.7 220.1 96L192 96C156.7 96 128 124.7 128 160L128 512C128 547.3 156.7 576 192 576L448 576C483.3 576 512 547.3 512 512L512 160C512 124.7 483.3 96 448 96L419.9 96z"/></svg>';
	const CHECK_ICON =
		'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 640" aria-hidden="true"><path d="M530.8 134.1C545.1 144.5 548.3 164.5 537.9 178.8L281.9 530.8C276.4 538.4 267.9 543.1 258.5 543.9C249.1 544.7 240 541.2 233.4 534.6L105.4 406.6C92.9 394.1 92.9 373.8 105.4 361.3C117.9 348.8 138.2 348.8 150.7 361.3L252.2 462.8L486.2 141.1C496.6 126.8 516.6 123.6 530.9 134z"/></svg>';

	function setCopyBtnIcon(/** @type {HTMLElement} */ btn, /** @type {string} */ icon) {
		btn.innerHTML = icon;
		const svg = btn.querySelector("svg");
		if (svg) {
			svg.style.cssText =
				"width: 1em; height: 1em; display: inline-block; vertical-align: -0.125em; fill: currentColor;";
		}
	}

	const copyBtn = document.createElement("span");
	copyBtn.className = "competitive-paste-copy";
	copyBtn.style.cssText =
		"margin-left: 0.2em; position: relative; bottom: 2px; cursor: pointer; font-weight: normal; white-space: nowrap; font-size: .8em; line-height: 1; vertical-align: middle;";
	copyBtn.title = "Create Files";
	setCopyBtnIcon(copyBtn, COPY_ICON);

	copyBtn.addEventListener("click", (event) => {
		event.preventDefault();
		event.stopPropagation();

		const samples = getSamples();
		const script = buildScript(samples);
		GM_setClipboard(script, "text");

		setCopyBtnIcon(copyBtn, CHECK_ICON);
		copyBtn.style.color = "#2e7d32";
		setTimeout(() => {
			setCopyBtnIcon(copyBtn, COPY_ICON);
			copyBtn.style.color = "unset";
		}, 2000);
	});

	titleEl.appendChild(copyBtn);
})();
```
