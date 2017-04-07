# Adding-Views-in-MFC
How to add views in MFC VC++

Views in MFC are nothing but the dialog box derived from CView class or CFormView class. Here we will see how we add CForm view in MFC using visual studio.

Steps to be followed:-

1. Run the visual studio(above VS10)
2. Create the project workspace.(I hope you know this else goto my link...)
3. You should create MDI application to add views.
4. Goto Resource view -> Dialog -> Add Resource(by right clicking on dialog)
5. small popup will come then expand the dialog and select Formview dialog
6. Now, Add the class to this dialog.
Note:- class must be derived from Form view.
7. Right click on dialog and select Add Class,select base class as CFormView, provide the name of the class and click finish.
8. Add the source code
