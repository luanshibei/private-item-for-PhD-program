Download all files(About 100M)
Double-click the main.exe
That's all
# Chapter 1: Software Development Background

## 1.1 Preface
Currently, software in the field of computational materials mainly focuses on a specific scale or only enables independent calculations across different scales. It fails to effectively integrate calculations from different scales, thus unable to bridge the gap between first-principles calculations and specific material applications. Combining microscopic computational data with practical material applications is a challenging task. There is an urgent need for software that can fulfill this function.

The cross-scale materials and devices integrated design, computation, and analysis software system (Software system for integrated computation, analysis and design of cross-scale materials and devices),简称MatDevCAD, is a software developed in Python. It integrates nine computational modules. Through phenomenological theory, it converts microscopic parameters obtained from first-principles calculation software into macroscopic physical quantities and further incorporates boundary conditions with the idea of finite element analysis for practical applications. The software includes a database system (with read-only/edit modes and a visual interface), an integrated design UI module, and integrated computational modules,etc.

## 1.2 Software Features
- Reflection/Absorption Coefficient Calculation Module (RAcoefficient)
- Optical Electric Field Calculation Module (OpticalEletricalField)
- Energy Dissipation Calculation Module (EnergyDissipation)
- Absorption Coefficient Calculation Module (AbsorptionCoefficient)
- Interface Photocurrent Calculation Module (InterOpticalCurrent)
- Short-Circuit Current Density Calculation Module (SCPD)
- Incident Photon Current Collection Efficiency Calculation Module (ICPE)
- ICPE Component Analysis Calculation (ICPEComponent)
- Automatic Optimal Solution Search Module (seekOptimalSolution)

## 1.3 Software Structure Diagram
The seven modules communicate with each other while being fully decoupled. The calculation part integrates the algorithms of the nine computational modules.

## 1.4 Operating Environment
- CPU: Intel Core i3 or above
- Memory: 256 MB, 512 MB recommended
- Disk: At least 50 MB of free space required on the system drive
- Display: Screen resolution of 800*600 or above, 1024*768 recommended (color settings of 256 colors or higher)

## 1.5 System Software and Programming Language
The software is developed in Python. Python interpreter is required to run py files. The software's algorithm part relies on the numpy library and the scipy library's interpolate module. The validator uses Python's built-in modules such as re, sys, os, and copy. The graphical user interface is built with PyQt5, incorporating some QSS style language, HTML language, and SQL database language. The plotting function is implemented with the high-quality plotting library matplotlib.

The software also provides a portable version with a pyinstaller-packaged .exe suffix, which is about 80 MB in size. On Windows, it can be run directly by double-clicking without installing additional dependent libraries. It can also be packaged into an .app application on the Mac system.

# Chapter 2: Software Interface

## 2.1 Welcome Interface and Initial Interface
### 2.1.1 Welcome Interface
The welcome interface is an irregular window featuring a multi-layer solar cell pattern along with the software name MatDevCAD, complemented by a solar halo effect, corresponding to the software's functionality. It is created using 3Dmax and Photoshop software.

### 2.1.2 Initial Interface
The initial interface is divided into five parts: menu bar, tool bar, status bar, database, and battery UI interface, as well as a workspace. The software opens in full-screen mode by default.

### 2.1.3 Initialization of Software Parameter Configuration
When the software is opened for the first time, it generates a configuration file named config.txt in the exe file's location and creates a database folder with a materials.db database file.

## 2.2 Menu Bar
The menu bar consists of five parts: File, Database, CellUI, Workshop, VASP, and About.
- The File menu includes functions like New Project.
- The Database menu includes database-related functions. When the software is opened, it automatically connects to the database in the project directory. If the database is open, clicking this option displays the database query mode window; if closed, it shows the edit mode window.
- The CellUI menu includes CellUI functions. When the software is opened, the solar cell UI interface is automatically launched. If the database is open, this option is grayed out. If the solar cell UI window is closed, this option becomes clickable.
- The Workshop menu includes Workshop functions. When the software is opened, the workspace interface is automatically launched. If the database is open, this option is grayed out. If the workspace window is closed, this option becomes clickable.
- The VASP menu includes functions like Add data from VASP data. When the software is opened, the workspace interface is automatically launched. If the database is open, this option is grayed out. If the workspace window is closed, this option becomes clickable.
- The About menu includes Contact Us functions. Clicking it pops up a dialog window displaying the author's contact information in HTML font style.

## 2.3 Toolbar (Including VASP File Post-processing Module)
The toolbar includes functions like New, Open, Save, Database, CellUI, Workshop, VASP, etc.
- When the software is initialized and opened, it automatically connects to the database in the project directory, launches the solar cell UI interface and workspace interface. If the database and workspace interfaces are open, the corresponding options are grayed out; when the windows are closed, the options become clickable.
- The VASP module can read the runVASP.xml and OUTCAR files output by the first-principles calculation software VASP, and perform post-processing to convert the incident photon energy and dielectric constant into corresponding wavelengths and reflection/absorption coefficients in the X, Y, and Z directions for model establishment and further calculations.

## 2.4 Status Bar
The status bar is located at the bottom of the screen, providing timely reminders of important information without interfering with user operations.

## 2.5 Other Features:
### 2.5.1 Dockable Toolbar
The toolbar can be easily dragged out or back, improving work efficiency.

### 2.5.2 Flexible Main Windows
The database, battery UI, and workspace windows support features like floating, docking, stretching, resizing, dragging borders, rearranging, folding, tiling, and individual opening/closing, making full use of screen space and significantly improving work efficiency.

# Chapter 3: Database Module

## 3.1 Edit Mode
### 3.1.1 Interface Style
The database module's initial interface is a form window. The three buttons are styled with QSS language for a fresh, elegant, and beautiful look.

### 3.1.2 Add, Delete, Query, and Modify Operations
- Clicking the Add a blank line button allows users to add a blank row. The * mark disappears upon successful addition, and the data can be saved and refreshed using the Save button in the toolbar.
- Clicking the Add data from files button imports data from files, supporting single and batch imports. Files are interpolated during import, and if a file is non-compliant, the software prompts the user to recheck the format. Currently, .csv and .txt files are supported.
- Select any row and click the Delete selected line button to delete it.
- The software supports sliding queries and fuzzy searches by material name. Entering a keyword in the search box and clicking Search highlights the first matching material's cell. Subsequent clicks on Search jump to the next matching material's cell, with the background deepening. The highlighting is cleared when switching to another keyword.
- To modify data, simply double-click the cell.

## 3.2 Query/Read-only Mode
In this mode, users can browse data by specified row numbers but cannot modify it. It supports displaying data by page, showing total records and page numbers, and flipping through or jumping to pages. Up to 50 rows can be displayed per page.

## 3.3 Interaction with CellUI Interface
The database interface has a right-click menu option to add materials to the solar cell's CellUI interface with one click. The menu options change based on the number of layers set in the CellUI interface.

## 3.4 Interaction with Status Bar
Clicking the right-click menu in the database interface not only changes the CellUI interface but also updates the status bar's prompt information. When materials are loaded into the model, the status bar displays "Sample import successfully." When the last material is loaded, it shows "All materials are ready!!!"

# Chapter 4: Integrated Design Module
## 4.1 Gradual Style Interface
### 4.1.1 Model Layer and Layer Thickness Settings
Supports calculating solar cell models with 1 to 10 layers. The interface uses a gradient color style based on RGB parameters without relying on image files, enhancing the software's robustness.

## 4.2 Interaction with Database
The layer thickness data of solar cells can be imported from the database via a right-click menu or manually entered and modified. These changes are not synchronized to the database to ensure data stability. When data is imported from the database into the CellUI interface, the material name and layer thickness are displayed, and the status bar provides corresponding prompts. When the last material is imported, the status bar indicates that all materials are ready, allowing the database window to be closed to free up space for model construction.

## 4.3 Model Construction and Destruction
### 4.3.1 Construction of Solar Cell UI Model
When all materials are imported, clicking the Build and Lock button prompts "Model construction successful" and locks the module. The label color turns gray, and the thickness cannot be edited or modified. The number of layers cannot be changed, and data cannot be cleared. The Build and Lock button turns dark purple with red font and border, and the text changes to Reset and Unlock. The module enters a locked state.
### 4.3.2 Model Destruction and Clearing
This operation must be performed under an unlocked state. Clicking the Clear button clears the model data and resets it. The Clear button is placed away from the Build and Lock button to prevent accidental clicks.
### 4.3.3 Human-centered Design
When switching the number of layers, previously entered data is not deleted, whether it exceeds or is less than the current number of layers. This allows users to adjust the number of layers without re-entering data, improving the user experience.
If a material is added incorrectly, simply re-add the material at the corresponding position in the database to overwrite the original data.
The Clear button is also placed away from the Build and Lock button to prevent users from accidentally clearing all data. When materials are imported, the status bar updates accordingly.

## 4.4 Robustness
The software's robustness is reflected in its ability to handle illegal operations stably. As mentioned earlier, material data can be covered and retained, and the model is locked after construction. Additionally, the layer thickness input box is equipped with a custom validator based on regular expressions to prevent illegal inputs. When users attempt to construct a model without entering all material information, a dialog box reminds them.

# Chapter 5: Workspace Module
## 5.1 Brief Introduction to the Module
When the model is not constructed, the menu bar is grayed out. After successfully clicking the Build and Lock button, the menu bar unlocks, and the solar cell interface locks. The workspace module's menu bar is divided into integrated calculation options and window view options. The window view options include tile and cascade modes.

## 5.2 Integrated Calculation Module (9 Major Calculation Modules)
The integrated calculation module consists of nine sub-modules: Reflection/Absorption Coefficient Calculation Module, Optical Electric Field Calculation Module, Energy Dissipation Calculation Module, Absorption Coefficient Calculation Module, Interface Photocurrent Calculation Module, Short-Circuit Current Density Calculation Module, Incident Photon Current Collection Efficiency Calculation Module (ICPE), ICPE Component Analysis Calculation, and Automatic Optimal Solution Search Module.
Since the software uses deep copying, models between modules and within the same module's windows are independent, enabling parallel calculations.

## 5.3 Reflection/Absorption Coefficient Calculation Module
This module takes a certain solar cell as an example. The initial interface features a canvas on the left and a row of controls on the right. The window can be stretched or shrunk but cannot exceed the workspace window. This module allows users to set wavelength ranges and steps to calculate absorption and reflection coefficients at different wavelengths. Clicking the Run button starts the calculation and displays the optimal absorption wavelength. The input box is equipped with a validator to prevent illegal inputs.
The module automatically labels tags and uses matplotlib for automatic coloring and high-quality image generation. After calculation, a Save button appears. Clicking it creates an RAcoefficient directory in the project directory and saves data and high-quality images. Data files (RAcoefficient) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving.

## 5.4 Optical Electric Field Calculation Module
This module takes a certain solar cell as an example. The initial interface features a canvas on the left and a row of controls on the right. The window can be stretched or shrunk but cannot exceed the workspace window. This module allows users to set wavelength ranges and material thicknesses to calculate the optical electric field distribution. Clicking the Run button starts the calculation. The input box is equipped with a validator to prevent illegal inputs.
The module automatically grids and uses matplotlib for automatic coloring and high-quality image generation. After calculation, a Save button appears. Clicking it creates an OpticalEletricalField directory in the project directory and saves data and high-quality images. Data files (OpticalEletricalField) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving.

## 5.5 Energy Dissipation Calculation Module
This module takes a certain solar cell as an example. The initial interface features a canvas on the left and a row of controls on the right. The window can be stretched or shrunk but cannot exceed the workspace window. This module allows users to set wavelength ranges and material thicknesses to calculate the energy dissipation distribution. Clicking the Run button starts the calculation. The input box is equipped with a validator to prevent illegal inputs.
The module automatically grids and uses matplotlib for automatic coloring and high-quality image generation. After calculation, a Save button appears. Clicking it creates an EnergyDissipation directory in the project directory and saves data and high-quality images. Data files (EnergyDissipation) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving.

## 5.6 Absorption Coefficient Calculation Module
This module takes a certain solar cell as an example. The initial interface features a canvas on the left and a row of controls on the right. The window can be stretched or shrunk but cannot exceed the workspace window. This module allows users to set wavelength ranges and steps and supports calculating six materials simultaneously. Clicking the Run button starts the calculation. The input box is equipped with a validator to prevent illegal inputs.
The module automatically labels tags and uses matplotlib for automatic coloring and high-quality image generation. After calculation, a Save button appears. Clicking it creates an AbsorptionCoefficient directory in the project directory and saves data and high-quality images. Data files (AbsorptionCoefficient) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving.

## 5.7 Interface Photocurrent Calculation Module
This module takes a certain solar cell as an example. The initial interface features a canvas on the left and a row of controls on the right. The window can be stretched or shrunk but cannot exceed the workspace window. This module allows users to set wavelengths and supports calculating interface photocurrents for six specified thicknesses. Clicking the Run button starts the calculation. The input box is equipped with a validator to prevent illegal inputs.
The module automatically labels tags and uses matplotlib for automatic coloring and high-quality image generation. After calculation, a Save button appears. Clicking it creates an InterOpticalCurrent directory in the project directory and saves data and high-quality images. Data files (InterOpticalCurrent) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving.

## 5.8 Short-Circuit Current Density Calculation Module
This module takes a certain solar cell as an example. It allows users to set wavelength ranges and steps and supports calculating short-circuit current densities for six specified thicknesses. Clicking the Run button starts the calculation. The input box is equipped with a validator to prevent illegal inputs. The module automatically reads materials with exciton diffusion length parameters from the user-generated model and displays them in a dropdown control, with checkboxes changing accordingly for users to select boundary conditions.
The module automatically labels tags and uses matplotlib for automatic coloring and high-quality image generation. After calculation, a Save button appears. Clicking it creates an SCPD directory in the project directory and saves data and high-quality images. Data files (SCPD) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving.

## 5.9 Incident Photon Current Collection Efficiency Calculation Module (ICPE)
This module takes a certain solar cell as an example. It allows users to set wavelength ranges and steps and supports calculating ICPE for six specified thicknesses. Clicking the Run button starts the calculation. The input box is equipped with a validator to prevent illegal inputs. The module automatically reads materials with exciton diffusion length parameters from the user-generated model and displays them in a dropdown control, with checkboxes changing accordingly for users to select boundary conditions.
The module automatically labels tags and uses matplotlib for automatic coloring and high-quality image generation. After calculation, a Save button appears. Clicking it creates an ICPE directory in the project directory and saves data and high-quality images. Data files (ICPE) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving.

## 5.10 ICPE Component Analysis Calculation
This module takes a certain solar cell as an example. It allows users to set wavelength ranges and steps and supports ICPE component analysis for specified material thicknesses. Clicking the Run button starts the calculation. The input box is equipped with a validator to prevent illegal inputs. The module automatically reads materials with exciton diffusion length parameters from the user-generated model and displays them in a dropdown control, with checkboxes changing accordingly for users to select boundary conditions.
The module automatically labels tags and uses matplotlib for automatic coloring and high-quality image generation. After calculation, a Save button appears. Clicking it creates an ICPEComponent directory in the project directory and saves data and high-quality images. Data files (ICPEComponent) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving.

## 5.11 Automatic Optimal Solution Search Module
This module takes a certain solar cell as an example. It allows users to set wavelength ranges and steps and supports ICPE component analysis with two specified material thickness ranges and steps. Clicking the Run button starts the calculation. The input box is equipped with a validator to prevent illegal inputs. The module automatically reads materials with exciton diffusion length parameters from the user-generated model and displays them in a dropdown control, with checkboxes changing accordingly for users to select boundary conditions. A progress bar is also provided for users to monitor the calculation progress.
The module automatically labels tags and uses matplotlib for automatic coloring and high-quality 3D image generation. After calculation, a Save button appears. Clicking it creates a seekOptimalSolution directory in the project directory and saves data and high-quality images. Data files (seekOptimalSolution) are saved in txt format with # comments for headers and other information, which can be opened with Notepad and used by other software. The status bar displays a prompt upon successful saving. If users find the calculation too heavy or slow and wish to reset, they can simply click Cancel to stop the current task and reset.

## 5.12 Multi-threaded Calculation
The software supports multi-window calculations within the same module, simultaneous calculations across multiple modules, and even multi-module multi-window calculations. All calculation modules support multi-threaded calculations to enhance the user experience.
