
# Creating a print queue

## Allowing File Devices Access to Printer

```bash
sudo sed -i 's/#FileDevice No/FileDevice Yes/' /home/adarsh/cups/conf/cups-files.conf
```
- `sed -i 's/#FileDevice No/FileDevice Yes/' /home/adarsh/cups/conf/cups-files.conf`: Replace `#FileDevice No` with `FileDevice Yes` in `/home/adarsh/cups/conf/cups-files.conf.`
- Also build again to make changes to take effect.

## Adding a Virtual Printer

```bash#
/home/adarsh/cups/build/sbin/lpadmin -p MyVirtualPrinter -E -v file:/home/adarsh/output.pdf
```
- `/home/adarsh/cups/build/sbin/lpadmin` : Path for `lpadmin` in CUPS.
- `-p MyVirtualPrinter` : Specifies the name of the printer.
- `-E` : Enables the printer. 
- `-v file:/home/adarsh/output.pdf` : Sets the URI for the printer using a file backend. In this case, output.pdf does not exist, effectively simulating a null backend or a non-existent file.

## Printing a File to the Virtual Printer

```bash
/home/adarsh/cups/build/bin/lp -d MyVirtualPrinter /home/adarsh/Downloads/Res.pdf
```
- `/home/adarsh/cups/build/bin/lp` : Path for `lp` in CUPS.
- `-d MyVirtualPrinter` : Specifies the name of the printer.
- `/home/adarsh/Downloads/Res.pdf` : The file to be printed.

Output:
```bash
request id is MyVirtualPrinter-15 (1 file(s))
```
This command sends a print job to the virtual printer `MyVirtualPrinter.` The request ID, in this case, is `MyVirtualPrinter-15,` and it indicates that one file is in the print job. The use of a non-existent file (output.pdf) in the virtual printer setup simulates a null backend, effectively discarding the print job data without generating any physical output.

Note: If using a network printer with a URI in place of null backend like `ipp://11.22.33.44/ipp/print,` it may keep running and searching for the printer without generating immediate output, especially if the printer is not available or reachable.
