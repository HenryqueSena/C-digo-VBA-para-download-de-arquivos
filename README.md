# C-digo-VBA-para-download-de-arquivos
Eu criei um código em VBA Outlook para a empresa Cruzeiro do Sul
Public Sub anexos_BAIXADOS()
Dim OutlookApplication As Object
Dim myItem As Outlook.Inspector
Dim objItem As Object
Dim CMails As Outlook.Items
Dim olMail As Outlook.MailItem
Dim Anexo As Outlook.Attachment
Dim VMails As Variant
Dim iItem
Dim i As Long
Dim ConferePasta As String
 ' o código possui criação de uma pasta automática impedindo a necessidade de trocar de diretório toda vez
 
ConferePasta = "(diretorio onde quer salvar)\NOVA PASTA"
 
If Dir(ConferePasta, vbDirectory) = "" Then
 
MkDir ConferePasta
 
MsgBox "O diretório: " & ConferePasta & " foi criado!", vbInformation, "AVISO"
 
End If

diretorio = "(diretorio onde quer salvar)\NOVA PASTA\"

Set OutlookApplication = GetOutlookApplication

If OutlookApplication Is Nothing Then Exit Sub
' se tiver alguma subpasta, adicionar outra .Folders("e aqui dentro o nome da pasta")
Set CMails = OutlookApplication.Session.Folders("email intitucional").Folders("nome da pasta").Folders("nome da pasta").Folders("nome da pasta").Items
ReDim VMails(1 To CMails.Count, 0 To 1)
For i = 1 To CMails.Count
Set iItem = CMails.Item(i)

If TypeName(iItem) <> "MailItem" Then GoTo NextItem

qtd_anexo = 0
For Each Anexo In iItem.Attachments
qtd_anexo = qtd_anexo + 1
Anexo.SaveAsFile diretorio & Anexo.FileName

Next Anexo

NextItem:
Next i

MsgBox ("Macro finalizada :)")

End Sub
Public Function GetOutlookApplication() As Outlook.Application
Dim OutlookApplication As Outlook.Application
On Error Resume Next
Set OutlookApplication = GetObject("", "Outlook.Application")
On Error GoTo 0
If OutlookApplication Is Nothing Then
Set OutlookApplication = CreateObject("Outlook.Application")
End If
If OutlookApplication Is Nothing Then
MsgBox "Favor abrir o Outlook antes de prosseguir!", vbExclamation
End If
Set GetOutlookApplication = OutlookApplication
End Function
