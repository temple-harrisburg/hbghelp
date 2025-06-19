---
tags:
  - adobe
  - acrobat
  - pdf
  - forms
published: true
---
There are many situations where you need a standardized form where recipients can input information digitally instead of on paper. PDF forms are perfect for these scenarios.

This article won't go into creating a form from scratch— it only focuses on adding fields. You can create the form template in a program you're comfortable with (Microsoft Word, Excel, Publisher, etc...) and then export it as a PDF.

## Open the PDF Document

1. Open Adobe Acrobat and open a PDF.
2. In the 'Tools' Tab, select 'Prepare Form'

![This image has an empty alt attribute; its file name is Pasted-image-20230309114804-1024x745.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309114804-1024x745.png)

3. Choose the PDF you want to turn into a form.
4. Uncheck the box next to "Automatically detect Form fields," then click 'OK'

![This image has an empty alt attribute; its file name is Pasted-image-20230309115053-1024x649.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309115053-1024x649.png)

5. Click 'Start'

## Creating form fields

1. To create new text fields, select the **Text Field tool** from the **Prepare Form** toolbar at the top of the window.

![This image has an empty alt attribute; its file name is Pasted-image-20230309120639.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309120639.png)

2. Click on any location in the document to place a form field.

![This image has an empty alt attribute; its file name is Pasted-image-20230309120716.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309120716.png)

3. Enter a name for your field.
    - **Optional**: If you plan on having similar fields on other pages, use some naming scheme to distinguish this field from the fields on other pages. Naming conventions help you keep track of the purpose of each field.

![This image has an empty alt attribute; its file name is Pasted-image-20230309121215.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309121215.png)

3. Resize the field to your desired specification using the control points (solid white dots) at the corners and midpoints of the field's bounding box.

![This image has an empty alt attribute; its file name is Pasted-image-20230309121711.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309121711.png)

With this method, you can create PDF forms with many different interactable elements, including text fields, checkboxes, 'radio' inputs and sliders. This is good enough to create a few fields, but if you need to create a large amount of precisely-placed fields, Acrobat also has tools to help.

## Creating Grids of Unique Form Fields

### "Unique" form fields?

- If you copy and paste a form field, Adobe Acrobat will interpret the original and the copied fields as "**linked**"
- "Linked" means that the data entered by a viewer of the form into one field will also show up in the other field.
- If we need a large amount of precisely placed unique form fields, we can use Acrobat's '**Create Multiple Copies…**' feature.

### 'Create Multiple Copies…'

For this process, the first form field should be placed in the topmost left cell of your grid.

1. Right click the field and select 'Create Multiple Copies'

![](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309124629.png)

2. The 'Create Multiple Copies of Fields' dialog box should open, and you should see blue rectangles similar to your original field in a 2x2 grid.

![](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309124706.png)

---

#### "Create Multiple Copies" Parameters Explained

![](https://sites.temple.edu/hbghelp/files/2023/12/image-6.png)

- **Number of Fields:**
    - Copy selected fields down:
        - The total number of 'rows' of copied fields, including the original field.
    - Copy selected fields across:
        - The total number of 'columns' of copied fields, including the original field.
- **Overall Size** (All Fields):
    - The height and width of the area over which the 'grid' of fields will be generated.
    - Changing the Width and Height will change the distance between the field copies.
- **Overall Position** (All Fields):
    - Click on the Up, Left, Right, and Down buttons shifts the area over which the 'grid' of fields.
    - The distance between field copies is not affected.

### Creating the grid

3. On this specific page, we need 2 'columns' and 13 'rows' of fields. Click the 'Up' arrow on the number field next to 'Copy selected fields down' to create 13 rows.

![This image has an empty alt attribute; its file name is Pasted-image-20230309125613.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309125613.png)

4. Click the up arrow next to 'Change Height' to increase the distance between fields. The last field should match the last cell of our grid.
    - **_TIP_**: Holding 'Shift' when clicking the up or down arrows on the number field increments the field by a greater number, allowing you to increase the distance faster.

![This image has an empty alt attribute; its file name is Pasted-image-20230309125731.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309125731.png)

5. Following the same method as step 4, increase the width to align the columns with our document's grid.

![This image has an empty alt attribute; its file name is Pasted-image-20230309130202-1024x776.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309130202-1024x776.png)

6. Click 'OK'. You should now have a grid of form fields with different names.

### Fixing the Alignment

- The 'Create Multiple Copies…' dialogue did not align perfectly with our form's grid. We need to fix this manually.
- Also, we still haven't created fields for the other columns of our PDF. This is intentional. Once we align the first column, it will be easier to align all the other fields we create.

---

1. Select the fields in the **_first column_** of our grid and begin moving and resizing them to fit the original PDF's grid. **_Only do this for the first column_**.
    - The fields do not have to be aligned perfectly yet.

![This image has an empty alt attribute; its file name is Pasted-image-20230309130834.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309130834.png)

2. Once all the fields are aligned to the cells of the original PDF, select the first field again. Then, use the mouse pointer to draw a rectangle around all the fields of **_just the first column_** to select them.

![This image has an empty alt attribute; its file name is Pasted-image-20230309131354.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309131354.png)

1. In the top of the right-hand sidebar, under the selection of icons labeled 'Align', select the icon that shows items aligned vertically.

![This image has an empty alt attribute; its file name is Pasted-image-20230309131246.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309131246.png)

4. This perfectly aligns all the fields in our column with the first field that we selected.

### Aligning Rows

- Now that we have a column of perfectly aligned fields, we can repeat the 'Create Multiple Copies' process to fill in the rest of the form.

1. Repeat the 'Create Multiple Copies…' process above with your other field.
2. Using the pointer, draw a box around just the row of fields you want to align.

![This image has an empty alt attribute; its file name is Pasted-image-20230309132519-1024x257.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309132519-1024x257.png)

3. Under 'Match Size', click 'Match Height'

![This image has an empty alt attribute; its file name is Pasted-image-20230309133128.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309133128.png)

4. Under Align, Select 'Align Top', 'Align Center', or 'Align Bottom'. Any of them will have the same effect.

![This image has an empty alt attribute; its file name is Pasted-image-20230309133423.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309133423.png)

4. The row is now perfectly aligned to the original selected field.

![This image has an empty alt attribute; its file name is Pasted-image-20230309133324-1024x263.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309133324-1024x263.png)

6. Repeat this process for every row on the page. When you use the pointer to draw a rectangle to select the row, the leftmost field should automatically be 'activated' (highlighted in blue; see above).

![This image has an empty alt attribute; its file name is Pasted-image-20230309133702-1024x716.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309133702-1024x716.png)

7. Repeat this process for every page of your PDF. **_Do not copy and paste fields_**, as these fields will be 'linked' and will duplicate whatever the recipient of the PDF enters into one fields across multiple fields.
8. When you are done, click on the floppy disk icon in the top left corner to save your PDF.

![This image has an empty alt attribute; its file name is Pasted-image-20230309135742.png](https://sites.temple.edu/hbghelp/files/2023/12/Pasted-image-20230309135742.png)

---