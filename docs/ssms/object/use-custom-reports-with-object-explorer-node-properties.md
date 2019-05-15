---
title: 使用自訂報表搭配物件總管節點屬性 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: c7b84355-71ba-402d-85af-23826f18b7da
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a469266b493e1da741738984c1f99b2c1f755699
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095679"
---
# <a name="use-custom-reports-with-object-explorer-node-properties"></a>使用自訂報表搭配物件總管節點屬性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果自訂報表參考選定 [物件總管] 節點的報表參數，自訂報表就可以在該節點的內容中執行。 這可讓自訂報表使用目前的內容 (例如目前的資料庫) 或資料庫或伺服器物件。  
  
## <a name="object-explorer-node-report-parameters"></a>物件總管節點報表參數  
  
|參數名稱|資料類型|  
|------------------|-------------|  
|**ObjectName**|**字串**|  
|**ObjectTypeName**|**String**|  
|**已篩選**|**布林**|  
|**ServerName**|**String**|  
|**FontName**|**String**|  
|**DatabaseName**|**String**|  
  
## <a name="object-explorer-node-report-parameters-example"></a>物件總管節點報表參數範例  
若要執行範例，請使用下列程序。  
  
**在物件總管中檢視某個節點的報表參數值**  
  
1.  將下列範例程式碼複製到新的文字檔，然後使用 .rdl 副檔名來命名該檔案。  
  
2.  將報表檔案複製到您在資料庫伺服器上針對自訂報表所建立資料夾。  
  
3.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，於物件總管中的節點上按一下滑鼠右鍵，再指向 [報表]，然後按一下 [自訂報表]。 在 [開啟檔案] 對話方塊中，找出自訂報表資料夾並選取報表檔案，然後按一下 [開啟]。  
  
    第一次從物件總管節點開啟新的自訂報表時，該報表會新增到該節點的快速鍵功能表中，[自訂報表] 下之最近使用的清單中。 第一次開啟標準報表時，該報表也會顯示在 [自訂報表] 下之最近使用的清單中。 如果您刪除了某個自訂報表檔，下次選取該項目時，系統就會提示您是否要從最近使用清單中刪除該項目。  
  
    1.  若要變更最近使用之清單上所顯示的檔案數，請在 [工具] 功能表中按一下 [選項]，再展開 [環境] 資料夾，然後按一下 [一般]。  
  
    2.  調整 [顯示在最近使用的清單中的檔案數] 中的數目。  
  
## <a name="custom-report-code-sample"></a>自訂報表程式碼範例  
使用下列程式碼所建立的報表將會使用與 [物件總管] 節點相關聯的參數。  
  
```  
<pre><?xml version="1.0" encoding="utf-8"?>  
<Report xmlns="https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition" xmlns:rd="https://schemas.microsoft.com/SQLServer/reporting/reportdesigner">  
<ReportParameters>  
<ReportParameter Name="ObjectName">  
<DataType>String</DataType>  
<Nullable>true</Nullable>  
<AllowBlank>true</AllowBlank>  
<Prompt>ObjectName</Prompt>  
</ReportParameter>  
<ReportParameter Name="ObjectTypeName">  
<DataType>String</DataType>  
<Nullable>true</Nullable>  
<AllowBlank>true</AllowBlank>  
<Prompt>ObjectTypeName</Prompt>  
</ReportParameter>  
<ReportParameter Name="Filtered">  
<DataType>Boolean</DataType>  
<Nullable>true</Nullable>  
<AllowBlank>true</AllowBlank>  
<Prompt>Filtered</Prompt>  
</ReportParameter>  
<ReportParameter Name="ServerName">  
<DataType>String</DataType>  
<Nullable>true</Nullable>  
<AllowBlank>true</AllowBlank>  
<Prompt>ServerName</Prompt>  
</ReportParameter>  
<ReportParameter Name="FontName">  
<DataType>String</DataType>  
<DefaultValue>  
<Values>  
<Value>Tahoma</Value>  
</Values>  
</DefaultValue>  
<AllowBlank>true</AllowBlank>  
<Prompt>FontName</Prompt>  
</ReportParameter>  
<ReportParameter Name="DatabaseName">  
<DataType>String</DataType>  
<Nullable>true</Nullable>  
<DefaultValue>  
<Values>  
<Value>master</Value>  
</Values>  
</DefaultValue>  
<AllowBlank>true</AllowBlank>  
<Prompt>DatabaseName</Prompt>  
</ReportParameter>  
</ReportParameters>  
<DataSources>  
<DataSource Name="AllReportParameters">  
<ConnectionProperties>  
<IntegratedSecurity>true</IntegratedSecurity>  
<ConnectString>Data Source=.</ConnectString>  
<DataProvider>SQL</DataProvider>  
</ConnectionProperties>  
<rd:DataSourceID>f1feee4c-0fdc-4301-9efa-3cd89eed2d9f</rd:DataSourceID>  
</DataSource>  
</DataSources>  
<BottomMargin>1in</BottomMargin>  
<RightMargin>1in</RightMargin>  
<rd:DrawGrid>true</rd:DrawGrid>  
<InteractiveWidth>8.5in</InteractiveWidth>  
<rd:SnapToGrid>true</rd:SnapToGrid>  
<Body>  
<ReportItems>  
<Textbox Name="textbox1">  
<rd:DefaultName>textbox1</rd:DefaultName>  
<ZIndex>1</ZIndex>  
<Width>6in</Width>  
<Style>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>20pt</FontSize>  
<Color>SteelBlue</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Height>0.36in</Height>  
<Value>AllReportParameters</Value>  
</Textbox>  
<Table Name="table1">  
<DataSetName>AllReportParameters</DataSetName>  
<Top>0.36in</Top>  
<Details>  
<TableRows>  
<TableRow>  
<TableCells>  
<TableCell>  
<ReportItems>  
<Textbox Name="ObjectName">  
<rd:DefaultName>ObjectName</rd:DefaultName>  
<ZIndex>5</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!ObjectName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="ObjectTypeName">  
<rd:DefaultName>ObjectTypeName</rd:DefaultName>  
<ZIndex>4</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!ObjectTypeName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="Filtered">  
<rd:DefaultName>Filtered</rd:DefaultName>  
<ZIndex>3</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!Filtered.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="ServerName">  
<rd:DefaultName>ServerName</rd:DefaultName>  
<ZIndex>2</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!ServerName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="FontName">  
<rd:DefaultName>FontName</rd:DefaultName>  
<ZIndex>1</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!FontName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="DatabaseName">  
<rd:DefaultName>DatabaseName</rd:DefaultName>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!DatabaseName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
</TableCells>  
<Height>0.21in</Height>  
</TableRow>  
</TableRows>  
</Details>  
<Header>  
<TableRows>  
<TableRow>  
<TableCells>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox2">  
<rd:DefaultName>textbox2</rd:DefaultName>  
<ZIndex>11</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>ObjectName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox3">  
<rd:DefaultName>textbox3</rd:DefaultName>  
<ZIndex>10</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>ObjectTypeName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox4">  
<rd:DefaultName>textbox4</rd:DefaultName>  
<ZIndex>9</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>Filtered</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox5">  
<rd:DefaultName>textbox5</rd:DefaultName>  
<ZIndex>8</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>ServerName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox6">  
<rd:DefaultName>textbox6</rd:DefaultName>  
<ZIndex>7</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>FontName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox7">  
<rd:DefaultName>textbox7</rd:DefaultName>  
<ZIndex>6</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>DatabaseName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
</TableCells>  
<Height>0.22in</Height>  
</TableRow>  
</TableRows>  
<RepeatOnNewPage>true</RepeatOnNewPage>  
</Header>  
<TableColumns>  
<TableColumn>  
<Width>3in</Width>  
</TableColumn>  
<TableColumn>  
<Width>1.5in</Width>  
</TableColumn>  
<TableColumn>  
<Width>0.75in</Width>  
</TableColumn>  
<TableColumn>  
<Width>1.125in</Width>  
</TableColumn>  
<TableColumn>  
<Width>2in</Width>  
</TableColumn>  
<TableColumn>  
<Width>1.375in</Width>  
</TableColumn>  
</TableColumns>  
</Table>  
</ReportItems>  
<Height>0.79in</Height>  
</Body>  
<rd:ReportID>abb14e58-fd36-495a-89ff-b66f29ef287b</rd:ReportID>  
<LeftMargin>1in</LeftMargin>  
<DataSets>  
<DataSet Name="AllReportParameters">  
<Query>  
<rd:UseGenericDesigner>true</rd:UseGenericDesigner>  
<CommandText>SELECT 1  
</CommandText>  
<DataSourceName>AllReportParameters</DataSourceName>  
</Query>  
<Fields>  
<Field Name="ObjectName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>ObjectName</DataField>  
</Field>  
<Field Name="ObjectTypeName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>ObjectTypeName</DataField>  
</Field>  
<Field Name="Filtered">  
<rd:TypeName>System.Boolean</rd:TypeName>  
<DataField>Filtered</DataField>  
</Field>  
<Field Name="ServerName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>ServerName</DataField>  
</Field>  
<Field Name="FontName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>FontName</DataField>  
</Field>  
<Field Name="DatabaseName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>DatabaseName</DataField>  
</Field>  
</Fields>  
</DataSet>  
</DataSets>  
<Width>6.875in</Width>  
<InteractiveHeight>11in</InteractiveHeight>  
<Language>en-US</Language>  
<TopMargin>1in</TopMargin>  
</Report></pre>  
```

## <a name="see-also"></a>另請參閱  
[Management Studio 中的自訂報表](../../ssms/object/custom-reports-in-management-studio.md)  
[將自訂報表加入 Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[取消隱藏執行自訂報表警告](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
  
