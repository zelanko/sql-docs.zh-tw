---
title: 步驟 1︰設定 Node.js 開發的開發環境 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce89cc12c7493522de55adffb69fcbe3307cbdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003756"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>步驟 1︰設定 Node.js 開發的開發環境
您必須使用必要條件設定您的開發環境, 才能使用 SQL Server 的 node.js 驅動程式來開發應用程式。  最常見的方法是使用 node package manager (npm) 來安裝繁瑣的模組, 但如果您想要的話, 可以直接在[Github](https://github.com/pekim/tedious)下載繁瑣的模組。  
  
請注意, node.js 驅動程式會使用 TDS 通訊協定, 其預設會在 SQL Server 和 Azure SQL Database 中啟用。  不需要進行其他組態設定。  
  
## <a name="windows"></a>Windows  
  
1. **安裝 node.js 執行時間和 npm 套件管理員**  
A. 前往[node.js](https://nodejs.org/en/download/)  
B. 按一下適當的 Windows installer msi 連結。   
c. 下載完成後, 請執行 msi 以安裝 node.js  
  
2. **開啟 cmd.exe**  
  
3. **建立專案目錄**, 並流覽至它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **建立節點專案。**  若要在專案建立期間保留預設值, 請在建立專案之前按下 enter。 在此步驟結束時, 您應該會在您的專案目錄中看到一個 package. json 檔案。  
```  
> npm init  
```  
  
5. **在您的專案中安裝繁瑣的模組。**  這是驅動程式用來與 SQL Server 進行通訊的 TDS 通訊協定的執行。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **開啟終端機**  
  
2. **安裝 node.js 執行時間**  
```  
>sudo apt-get install node  
```  
3. **安裝 npm (node package manager)**  
```  
> sudo apt-get install npm  
```  
4. **建立專案目錄**, 並流覽至它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **建立節點專案。**  若要在專案建立期間保留預設值, 請在建立專案之前按下 enter。 在此步驟結束時, 您應該會在您的專案目錄中看到一個 package. json 檔案。  
```  
> sudo npm init  
```  
  
6. **在您的專案中安裝繁瑣的模組。**  這是驅動程式用來與 SQL Server 進行通訊的 TDS 通訊協定的執行。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **安裝 node.js 執行時間和 npm 套件管理員**  
A. 前往[node.js](https://nodejs.org/en/download/)  
B. 按一下適當的 [Mac OS 安裝程式] 連結。  
c. 下載完成後, 請執行 dmg 來安裝 node.js  
  
2. **開啟終端機**  
  
3. **建立專案目錄**, 並流覽至它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **建立節點專案。**  若要在專案建立期間保留預設值, 請在建立專案之前按下 enter。 在此步驟結束時, 您應該會在您的專案目錄中看到一個 package. json 檔案。  
```  
> npm init  
```  
  
5. **在您的專案中安裝繁瑣的模組。**  這是驅動程式用來與 SQL Server 進行通訊的 TDS 通訊協定的執行。  
```  
> npm install tedious  
```  
  
