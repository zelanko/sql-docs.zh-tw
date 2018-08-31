---
title: 步驟 1︰ 設定 pyodbc Python 開發環境 |Microsoft Docs
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f588174ea80677066628cb3e756d7c38bd42fba
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2018
ms.locfileid: "42784908"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>步驟 1︰設定 pyodbc Python 開發的開發環境

## <a name="windows"></a>Windows  
使用 Python-在 Windows 上的 pyodbc 連接到 SQL Database:
  
1. **下載 Python 安裝程式**。  
  如果您的電腦並沒有 Python，請安裝它。 移至[的 Python 下載頁面](https://www.python.org/downloads/windows/)及下載適當的安裝程式。 例如，如果您是在 64 位元電腦上，下載 Python 2.7] 或 [3.7 (x64) 安裝程式。  
  
2. **安裝 Python**。  安裝程式下載後，執行下列步驟：。 按兩下檔案以啟動安裝程式。 B. 選取您的語言，並同意條款。 c. 遵循螢幕上的指示，並應該在電腦上安裝 Python。 d. 您可以確認要安裝 Python`C:\Python27`或是`C:\Python37`並執行`python -V`或`py -V`（適用於 3.x) 
      
3. [**安裝 Windows 上的 Microsoft ODBC Driver for SQL Server**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **系統管理員身分開啟 cmd.exe**     

5. **安裝 pyodbc 使用 pip-Python 套件管理員**(取代`C:\Python27\Scripts`以您已安裝的 Python 路徑)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
使用 Python-pyodbc 連接到 SQL Database:
  
1. **開啟終端機**  

2. [**在 Linux 上安裝 Microsoft ODBC Driver for SQL Server**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **安裝 pyodbc**  
```  
> sudo -H pip install pyodbc
```
