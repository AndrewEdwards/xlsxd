# libxlsxd

A small wrapper in the D programming language around the C library
libxlsxwriter, which writes Excel spreadsheets.

## Example

```D
import libxlsxd;

void main() {
    /* Create a new workbook and add a worksheet. 
	Workbook is RefCounted and will write the file
	when it is released.
	*/
    auto workbook  = newWorkbook("demo.xlsx");
    auto worksheet = workbook.addWorksheet(null);

    /* Add a format. */
    auto format = workbook.addFormat();

    /* Set the bold property for the format */
    format.setBold();

    /* Change the column width for clarity. */
    worksheet.setColumn(0, 0, 20);

    /* Write some simple text. */
    worksheet.writeString(0, 0, "Hello");

    /* Text with formatting. */
    worksheet.writeString(1, 0, "World", format);

    /* Write some numbers. */
    worksheet.writeNumber(2, 0, 123);
    worksheet.writeNumber(3, 0, 123.456);

	// for the lazy
    worksheet.write(4, 0, 13.37);
	// for the lazy
    worksheet.write(4, 1, true);

    worksheet.write(4, 2, "Hello 1337");
	worksheet.setColumn(4, 2, 20.0);
}
```

## API
Consult https://libxlsxwriter.github.io/index.html for the api documentation.

The D code:
```D
Workbook wb;
Format f = wb.addFormat();
```
is basically equivalent to this C code:
```C
lxw_workbook  *workbook
lxw_format *f = workbook_add_format(workbook);
```

So to find the documentation for the method "methodName" for the data structure
"Datastructure", search for a C function "toLower(Datastructure)\_toSnakeCase(methodName)".
In this example "datastructure\_method\_name".

About Kaleidic Associates
-------------------------
We are a boutique consultancy that advises a small number of hedge fund clients.  We are
not accepting new clients currently, but if you are interested in working either remotely
or locally in London or Hong Kong, and if you are a talented hacker with a moral compass
who aspires to excellence then feel free to drop me a line: laeeth at kaleidic.io

We work with our partner Symmetry Investments, and some background on the firm can be
found here:

http://symmetryinvestments.com/about-us/
