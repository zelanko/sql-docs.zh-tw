---
title: 步驟 1： 設定 pymssql Python 開發環境 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91b941785a6fe7788c9590efd9f9c42ac6c60b10
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>步驟 1： 設定 pymssql Python 開發的開發環境
您必須設定開發環境的必要條件，才能開發使用 Python Driver for SQL Server 的應用程式。    
  
請注意，Python SQL 驅動程式會使用 TDS 通訊協定，SQL Server 和 Azure SQL Database 中的預設會啟用。  不需要進行其他組態設定。  
  
## <a name="windows"></a>視窗  
  
1. **安裝 Python 執行階段以及 pip 封裝管理員**  
a. 移至[python.org](https://www.python.org/downloads/)  
b. 按一下適當的 Windows 安裝程式 msi 連結。   
c. 下載一次執行的 msi 安裝 Python 執行階段  
  
2. **下載模組說明 pymssql**從[這裡](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    請確定您選擇正確的 whl 檔案。  例如： 如果您在 64 位元電腦上使用 Python 2.7 選擇： pymssql‑2.1.1‑cp27‑none‑win_amd64.whl。 一旦您下載.whl 檔案將它放在 c: / Python27 資料夾。  
      
3. **開啟 cmd.exe**  
  
4. **安裝 pymssql 模組**     
    例如，如果您在 64 位元電腦上使用 Python 2.7:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **安裝 Python 執行階段以及 pip 封裝管理員**Python 上的 Ubuntu 多數散發變為預先安裝。  如果您的電腦沒有安裝 python，您可以取得任一下載從來源 tarball [python.org](https://www.python.org/downloads/)建置在本機，或您可以使用封裝管理員：  
```  
> sudo apt-get install python   
```  
  
2.  **開啟終端機**  
  
3.  **安裝 pymssql 模組相依性**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **安裝 Python 執行階段以及 pip 封裝管理員**  
a. 移至[python.org](https://www.python.org/downloads/)  
b. 按一下適當的 Mac installer byok-kek-pkg 連結。   
c. 下載一次執行安裝 Python 執行階段版本  
  
2.  **開啟終端機**  
  
3. **安裝 Homebrew 封裝管理員**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **安裝 freetds 才能使用模組**  
```  
> brew install FreeTDS  
```  
  
5.  **安裝 pymssql 模組**  
```  
> sudo -H pip install pymssql  
```
