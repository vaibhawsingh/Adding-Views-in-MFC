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
8. Add the source code.

Selection of class in which code is needed to be added.

A => In InitInstance of Application class Add this line of code

       pNewView = new CMultiDocTemplate(IDR_CViewsFormsTYPE,
		RUNTIME_CLASS(CCViewsFormsDoc),
		RUNTIME_CLASS(CChildFrame), // custom MDI child frame
		RUNTIME_CLASS(CNewView));
	if (!pNewView)
		return FALSE;
	AddDocTemplate(pNewView);
        
where pNewView is pointer of CMultiDocTemplate class declared in Header of Application class.
Uses of this code:-
It initializes and activate the newly added CFormView Dialog.

Now add the button either in menu bar or on ribbon bar to open the new view when the button is clicked.

To see how to add button please follow the link.........)

Add the event handler to that button and select the class as mainframe class.(event handler must be ON_COMMAND function)

B => In MainFrame class the new event handler which gets added, add this code there

    CMultiDocTemplate* pNewTemplate;
    CCViewsFormsApp * pApp = (CCViewsFormsApp*)AfxGetApp();//Accecs of Application class data
    POSITION pos;
    CMDIChildWnd* pFrame, *pMainView;
    CMainFrame *pMainWnd = (CMainFrame *)AfxGetMainWnd();//main frame window is called

    CCViewsFormsDoc* pDoc = (CCViewsFormsDoc*)GetDoc();//using this class pointer we fetche the document data of corresponding class
    if (NULL == pDoc)	//RP
      return;//return if no document is available

    pNewTemplate = theApp.pNewView;//object pointer of CMultiDocTemplate class associated with the newly added view class
    pos = pDoc->GetFirstViewPosition();//here it finds which view is on 1st position
    while (pos != NULL)//this loops removes each view untill it becomes null and it displayes the new view
    {
      CView* pView = pDoc->GetNextView(pos);
      if (pView->IsKindOf(RUNTIME_CLASS(CNewView)) == TRUE)
      {
        pFrame = (CMDIChildWnd*)pView->GetOwner();
        pFrame->MDIActivate();
        return;
      }
    }
    ASSERT_VALID(pNewTemplate);//here new view is inserted into view
    CMDIChildWnd* pNewFrame = (CMDIChildWnd*)pNewTemplate->CreateNewFrame(pDoc, NULL);
    ASSERT_VALID(pNewFrame);
    pNewTemplate->InitialUpdateFrame(pNewFrame, pDoc);


