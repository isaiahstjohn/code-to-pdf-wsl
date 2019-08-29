# code-to-pdf-wsl
A hacky way to get code from WSL into a PDF on Windows using GhostScript and enscript. The ultimate goal is to print a physical copy of the code, but I was unable to configure Ubuntu on WSL to use my networked printer. This allows me to instead print the code as a PDF from Windows.

## Prerequisites
Cmder must be installed on Windows and enscript must be installed on WSL

## Setup
1. Create a folder on Windows called, for example, `C:\box`.
2. On Windows, move the contents of `gs` to `%USERHOME%\cmder\bin`
3. On WSL, add the following lines or similar to your `.bashrc`:
```bash
function print(){
	enscript --line-numbers --language=PostScript --file-align=align -Ejavascript -hjr --columns=2 -p /mnt/c/box/out.ps "$@";
}
```
Save the file and in bash do `source ~/.bashrc`.
4. On Windows, in Cmder do `alias print=ps2pdf C:\box\out.ps C:\box\out.pdf`

## Usage
From WSL use `print some_source_code.cc` or `print *.js` to create an `out.ps` file in
`C:\box`. Then on Windows in Cmder do `print` to create an `out.pdf` file
in `C:\box`.

