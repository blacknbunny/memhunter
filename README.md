[![Build status](https://ci.appveyor.com/api/projects/status/aokyumj3hyx0i8cw/branch/master?svg=true)](https://ci.appveyor.com/project/marcosd4h/memhunter/branch/master)
[![Appveyor](https://badgen.net/appveyor/ci/marcosd4h/memhunter)](https://ci.appveyor.com/project/marcosd4h/memhunter)
[![Latest Commit](https://badgen.net/github/last-commit/marcosd4h/memhunter)](https://github.com/marcosd4h/memhunter/commits/master)
[![MIT license](https://badgen.net/badge/license/MIT/blue)](http://opensource.org/licenses/MIT)

# Memhunter
Live memory forensics hunter

Memhunter automates the hunting of memory resident malware, improving the threat hunter analysis process and remediation times. The tool detects and reports memory-resident malware living on endpoint processes. Memhunter only works on Windows at the moment, and it detects known malicious memory injection techniques. The detection process is performed through live analysis and without needing memory dumps. The tool was designed as a replacement of memory forensic volatility plugins such as malfind and hollowfind. The idea of not requiring memory dumps helps on performing the memory resident malware threat hunting at scale, without manual analysis, and without the complex infrastructure needed to move dumps to forensic environments.

In order to find footprints left by malware code injection techniques, memhunter relies on a set of memory inspection heuristics and ETW trace collection. Once a suspicious process gets identified, the tool filters out false-positives through Yara Rules analysis and VirusTotal queries. This down-selection process helps the tool to reduce the number of false positives, leaving only known-bad processes. The tool then gets forensic information on the remaining set of suspicious findings and report them back to the analyst for remediation steps.

The tool itself is a self-contained binary which can be run on the endpoint to conduct the memory hunting. The idea of a self-contained binary helps on reducing the footprint, the dependencies needed, and improving the deployability of the tool. The binary contains a set of embedded "hunters" plugins, each one in charge of performing a specific heuristic detection. It also contains the ability to register the binary as an ETW collection service, which will augment the findings of next runs by providing contextual information on the attack.
