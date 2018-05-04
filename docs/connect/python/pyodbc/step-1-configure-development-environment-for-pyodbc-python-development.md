---
title: 步驟 1： 設定 pyodbc Python 開發環境 |Microsoft 文件
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: beb0c34f5645615a69944088163ad157d59d3c3a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>步驟 1： 設定 pyodbc Python 開發的開發環境

## <a name="windows"></a>視窗  
使用 Python-pyodbc Windows 上，以連接到 SQL 資料庫：
  
1. **下載 Python 安裝程式**  
  如果您的電腦沒有 Python 請加以安裝。 移[Python 下載頁面](https://www.python.org/downloads/windows/)及下載適當的安裝程式。 如範例中，如果您是在 64 位元的電腦，下載 Python 2.7 或 3.5 (x64) 安裝程式。  
  
2. **安裝 Python**安裝程式下載後，執行下列動作：。 按兩下檔案以啟動安裝程式。 b. 選取語言，並同意這些條款。 c. 遵循螢幕上的指示和 Python 應該安裝在電腦上。 d. 您可以確認也就是 Python 安裝，請前往 C:\Python27 或 C:\Python35 與執行 python-v 或 py-v （用於 3.x) 
      
3. [**安裝 Microsoft ODBC 驅動程式**](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)
  
4. **系統管理員身分開啟 cmd.exe**     

5. **安裝使用 pip-pyodbc Python 封裝管理員**
```  
> cd C:\Python27\Scripts>  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
使用 Python-pyodbc Ubuntu 和 RedHat 上連接到 SQL 資料庫：
  
1. **開啟終端機**  

2. **安裝 Microsoft ODBC Driver 13 for Linux** Ubuntu 15.04 的 + 
``` 
> sudo su  
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-Ubuntu-b87369f0/file/154097/2/installodbc.sh  
> sh installodbc.sh  
```   

  用於 RedHat 6,7 
``` 
> sudo su 
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-SQL-8d067754/file/153653/4/install.sh 
> sh install.sh 
```  
  
3.  **安裝 pyodbc**  
```  
> sudo -H pip install pyodbc
```
