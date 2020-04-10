---
title: 步驟 1:設定 pymssql Python 開發環境 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3310f268bf04b015c5f80cd08b2ae3909fd3a5c2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926808"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>步驟 1:設定 pymssql Python 開發的開發環境
您將必須設定您的開發環境以符合先決條件，才能使用 Python Driver for SQL Server 開發應用程式。    
  
請注意，Python SQL 驅動程式會使用預設在 SQL Server 和 Azure SQL Database 中啟用的 TDS 通訊協定。  不需要進行其他組態設定。  
  
## <a name="windows"></a>Windows  
  
1. **安裝 Python 執行階段和 pip 套件管理員**  
a. 移至 [python.org](https://www.python.org/downloads/)  
b. 按一下適當的 Windows Installer msi 連結。   
c. 下載完成後，請執行 msi 以安裝 Python 執行階段  
  
2. **從[此處](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)下載 pymssql 模組**  
  
    確定您選擇正確的 whl 檔案。  例如：如果您在 64 位元電腦上使用 Python 2.7，請選擇：pymssql‑2.1.1‑cp27‑none‑win_amd64.whl。 在您下載 .whl 檔案之後，請將它放在 C:/Python27 資料夾中。  
      
3. **開啟 cmd.exe**  
  
4. **安裝 pymssql 模組**     
    例如，如果您在 64 位元電腦上使用 Python 2.7：  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **安裝 Python 執行階段和 pip 套件管理員** Python 已預先安裝在 Ubuntu 的大部分發行版本上。  如果您的電腦未安裝 Python，您可以從 [python.org](https://www.python.org/downloads/) 下載來源 tarball 並在本機建置，或者您可以使用套件管理員：  
```  
> sudo apt-get install python   
```  
  
2.  **開啟終端機**  
  
3.  **安裝 pymssql 模組和相依性**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **安裝 Python 執行階段和 pip 套件管理員**  
a. 移至 [python.org](https://www.python.org/downloads/)  
b. 按一下適當的 Mac 安裝程式 pkg 連結。   
c. 下載後，請執行 pkg 以安裝 Python 執行階段  
  
2.  **開啟終端機**  
  
3. **安裝 Homebrew 套件管理員**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **安裝 FreeTDS 模組**  
```  
> brew install FreeTDS  
```  
  
5.  **安裝 pymssql 模組**  
```  
> sudo -H pip install pymssql  
```
