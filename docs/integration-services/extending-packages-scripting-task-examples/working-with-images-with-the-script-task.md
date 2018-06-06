---
title: 以指令碼工作處理映像 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting-task-examples
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- graphics [Integration Services]
- Script task [Integration Services], images
- Drawing namespace
- images [Integration Services]
- SSIS Script task, images
- Script task [Integration Services], examples
- thumbnails [Integration Services]
- System.Drawing namespace
- JPEG format [Integration Services]
- .jpeg files
ms.assetid: 74aeb7ab-51b2-4b9f-84ee-0b46a7908ab9
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 664ac58f2423c1f4c603a32dff3892a3dde3db1c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-images-with-the-script-task"></a>以指令碼工作處理影像
  產品或是使用者的資料庫除了文字與數值資料之外經常包括影像。 Microsoft .NET Framework 中的 **System.Drawing** 命名空間提供操作影像的類別。  
  
 [範例 1：將影像轉換為 JPEG 格式](#example1)  
  
 [範例 2：建立和儲存縮圖影像](#example2)  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
##  <a name="example1"></a> 範例 1 描述：將影像轉換為 JPEG 格式  
 下列範例會開啟變數指定的影像檔，並使用編碼器將它儲存為壓縮的 JPEG 檔案。 擷取編碼器資訊的程式碼是封裝在私用函數中。  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>若要將指令碼工作範例設定成與單一影像檔搭配使用  
  
1.  建立名為 `CurrentImageFile` 的字串變數，並將其值設定為現有影像檔的路徑與檔案名稱。  
  
2.  在 [指令碼工作編輯器] 的 [指令碼] 頁面上，將 `CurrentImageFile` 變數加入 **ReadOnlyVariables** 屬性。  
  
3.  在指令碼專案中，設定 **System.Drawing** 命名空間的參考。  
  
4.  在程式碼中，使用 **Imports** 陳述式匯入 **System.Drawing** 和 **System.IO** 命名空間。  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>若要將指令碼工作範例設定成與多個影像檔搭配使用  
  
1.  在 Foreach 迴圈容器中置放指令碼工作。  
  
2.  在 **Foreach 迴圈編輯器** 的 [集合] 頁面上，將 [Foreach 檔案列舉值] 選取為列舉值，以及指定來源檔案的路徑與檔案遮罩，例如 "*.bmp"。  
  
3.  在 [變數對應] 頁面上，將 `CurrentImageFile` 變數對應至索引 0。 這個變數會在每次反覆運算列舉值時，將目前的檔案名稱傳遞給指令碼工作。  
  
    > [!NOTE]  
    >  除了列在用於單一影像檔之程序的步驟之外，這是額外的步驟。  
  
### <a name="example-1-code"></a>範例 1 程式碼  
  
```vb  
Public Sub Main()  
  
    'Create and initialize variables.  
    Dim currentFile As String  
    Dim newFile As String  
    Dim bmp As Bitmap  
    Dim eps As New Imaging.EncoderParameters(1)  
    Dim ici As Imaging.ImageCodecInfo  
    Dim supportedExtensions() As String = _  
        {".BMP", ".GIF", ".JPG", ".JPEG", ".EXIF", ".PNG", _  
        ".TIFF", ".TIF", ".ICO", ".ICON"}  
  
    Try  
        'Store the variable in a string for local manipulation.  
        currentFile = Dts.Variables("CurrentImageFile").Value.ToString  
        'Check the extension of the file against a list of  
        'files that the Bitmap class supports.  
        If Array.IndexOf(supportedExtensions, _  
            Path.GetExtension(currentFile).ToUpper) > -1 Then  
  
            'Load the file.  
            bmp = New Bitmap(currentFile)  
  
            'Calculate the new name for the compressed image.  
            'Note: This will overwrite existing JPEGs.  
            newFile = Path.Combine( _  
                Path.GetDirectoryName(currentFile), _  
                String.Concat(Path.GetFileNameWithoutExtension(currentFile), _  
                ".jpg"))  
  
            'Specify the compression ratio (0=worst quality, 100=best quality).  
            eps.Param(0) = New Imaging.EncoderParameter( _  
                Imaging.Encoder.Quality, 75)  
  
            'Retrieve the ImageCodecInfo associated with the jpeg format.  
            ici = GetEncoderInfo("image/jpeg")  
  
            'Save the file, compressing it into the jpeg encoding.  
            bmp.Save(newFile, ici, eps)  
        Else  
            'The file is not supported by the Bitmap class.  
            Dts.Events.FireWarning(0, "Image Resampling Sample", _  
                "File " & currentFile & " is not a supported format.", _  
                "", 0)  
         End If  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Image Resampling Sample", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Function GetEncoderInfo(ByVal mimeType As String) As Imaging.ImageCodecInfo  
  
    'The available image codecs are returned as an array,  
    'which requires code to iterate until the specified codec is found.  
  
    Dim count As Integer  
    Dim encoders() As Imaging.ImageCodecInfo  
  
    encoders = Imaging.ImageCodecInfo.GetImageEncoders()  
  
    For count = 0 To encoders.Length  
        If encoders(count).MimeType = mimeType Then  
            Return encoders(count)  
        End If  
    Next  
  
    'This point is only reached if a codec is not found.  
    Err.Raise(513, "Image Resampling Sample", String.Format( _  
        "The {0} codec is not available. Unable to compress file.", _  
            mimeType))  
    Return Nothing  
  
End Function  
  
```  
  
##  <a name="example2"></a> 範例 2 描述：建立和儲存縮圖影像  
 下列範例會開啟變數所指定的影像檔、建立影像的縮圖，同時維護固定的外觀比例，並以修改的檔案名稱儲存縮圖。 計算縮圖的高度與寬度並維持其固定外觀比例的程式碼，是封裝在私用副程式中。  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>若要將指令碼工作範例設定成與單一影像檔搭配使用  
  
1.  建立名為 `CurrentImageFile` 的字串變數，並將其值設定為現有影像檔的路徑與檔案名稱。  
  
2.  另外建立 `MaxThumbSize` 整數變數並指派以像素為單位的值，例如 100。  
  
3.  在**指令碼工作編輯器**的 [指令碼] 頁面上，將兩個變數都新增至 **ReadOnlyVariables** 屬性。  
  
4.  在指令碼專案中，設定 **System.Drawing** 命名空間的參考。  
  
5.  在程式碼中，使用 **Imports** 陳述式匯入 **System.Drawing** 和 **System.IO** 命名空間。  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>若要將指令碼工作範例設定成與多個影像檔搭配使用  
  
1.  在 Foreach 迴圈容器中置放指令碼工作。  
  
2.  在 **Foreach 迴圈編輯器**的 [集合] 頁面上，將 [Foreach 檔案列舉值] 選取為 [列舉值]，以及指定來源檔案的路徑與檔案遮罩，例如 "*.jpg"。  
  
3.  在 [變數對應] 頁面上，將 `CurrentImageFile` 變數對應至索引 0。 這個變數會在每次反覆運算列舉值時，將目前的檔案名稱傳遞給指令碼工作。  
  
    > [!NOTE]  
    >  除了列在用於單一影像檔之程序的步驟之外，這是額外的步驟。  
  
### <a name="example-2-code"></a>範例 2 程式碼  
  
```vb  
Public Sub Main()  
  
    Dim currentImageFile As String  
    Dim currentImage As Image  
    Dim maxThumbSize As Integer  
    Dim thumbnailImage As Image  
    Dim thumbnailFile As String  
    Dim thumbnailHeight As Integer  
    Dim thumbnailWidth As Integer  
  
    currentImageFile = Dts.Variables("CurrentImageFile").Value.ToString  
    thumbnailFile = Path.Combine( _  
        Path.GetDirectoryName(currentImageFile), _  
        String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), _  
        "_thumbnail.jpg"))  
  
    Try  
        currentImage = Image.FromFile(currentImageFile)  
  
        maxThumbSize = CType(Dts.Variables("MaxThumbSize").Value, Integer)  
        CalculateThumbnailSize( _  
            maxThumbSize, currentImage, thumbnailWidth, thumbnailHeight)  
  
        thumbnailImage = currentImage.GetThumbnailImage( _  
           thumbnailWidth, thumbnailHeight, Nothing, Nothing)  
        thumbnailImage.Save(thumbnailFile)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, "Script Task Example", _  
        ex.Message & ControlChars.CrLf & ex.StackTrace, _  
        String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Sub CalculateThumbnailSize( _  
    ByVal maxSize As Integer, ByVal sourceImage As Image, _  
    ByRef thumbWidth As Integer, ByRef thumbHeight As Integer)  
  
    If sourceImage.Width > sourceImage.Height Then  
        thumbWidth = maxSize  
        thumbHeight = CInt((maxSize / sourceImage.Width) * sourceImage.Height)  
    Else  
        thumbHeight = maxSize  
        thumbWidth = CInt((maxSize / sourceImage.Height) * sourceImage.Width)  
    End If  
  
End Sub  
```  
  
```csharp  
bool ThumbnailCallback()  
        {  
            return false;  
        }  
        public void Main()  
        {  
  
            string currentImageFile;  
            Image currentImage;  
            int maxThumbSize;  
            Image thumbnailImage;  
            string thumbnailFile;  
            int thumbnailHeight = 0;  
            int thumbnailWidth = 0;  
  
            currentImageFile = Dts.Variables["CurrentImageFile"].Value.ToString();  
            thumbnailFile = Path.Combine(Path.GetDirectoryName(currentImageFile), String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), "_thumbnail.jpg"));  
  
            try  
            {  
  
                currentImage = Image.FromFile(currentImageFile);  
  
                maxThumbSize = (int)Dts.Variables["MaxThumbSize"].Value;  
                CalculateThumbnailSize(maxThumbSize, currentImage, ref thumbnailWidth, ref thumbnailHeight);  
  
                Image.GetThumbnailImageAbort myCallback = new Image.GetThumbnailImageAbort(ThumbnailCallback);  
  
                thumbnailImage = currentImage.GetThumbnailImage(thumbnailWidth, thumbnailHeight, ThumbnailCallback, IntPtr.Zero);  
                thumbnailImage.Save(thumbnailFile);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
  
        private void CalculateThumbnailSize(int maxSize, Image sourceImage, ref int thumbWidth, ref int thumbHeight)  
        {  
  
            if (sourceImage.Width > sourceImage.Height)  
            {  
                thumbWidth = maxSize;  
                thumbHeight = (int)(sourceImage.Height * maxSize / sourceImage.Width);  
            }  
            else  
            {  
                thumbHeight = maxSize;  
                thumbWidth = (int)(sourceImage.Width * maxSize / sourceImage.Height);  
  
            }  
  
        }  
  
```  
  
  
