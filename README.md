# Magicodes.IE | [简体中文](README.zh-CN.md)
[![nuget](https://img.shields.io/nuget/v/Magicodes.IE.Core.svg?style=flat-square)](https://www.nuget.org/packages/Magicodes.IE.Core) 
[![stats](https://img.shields.io/nuget/dt/Magicodes.IE.Core.svg?style=flat-square)](https://www.nuget.org/stats/packages/Magicodes.IE.Core?groupby=Version)

## Overview

Import and export general library, support Dto import and export, template export, fancy export and dynamic export, support Excel, Csv, Word, Pdf and Html.

**![General description](./docs/Magicodes.IE.en.png)**

### Nuget

#### Stable version (recommended)

| **Name** | **Nuget** |
|----------|:-------------:|
| **Magicodes.IE.Core** | **[![NuGet](https://buildstats.info/nuget/Magicodes.IE.Core)](https://www.nuget.org/packages/Magicodes.IE.Core)** |
| **Magicodes.IE.Excel** | **[![NuGet](https://buildstats.info/nuget/Magicodes.IE.Excel)](https://www.nuget.org/packages/Magicodes.IE.Excel)**   |
| **Magicodes.IE.Pdf** | **[![NuGet](https://buildstats.info/nuget/Magicodes.IE.Pdf)](https://www.nuget.org/packages/Magicodes.IE.Pdf)**   |
| **Magicodes.IE.Word** | **[![NuGet](https://buildstats.info/nuget/Magicodes.IE.Word)](https://www.nuget.org/packages/Magicodes.IE.Word)**   |
| **Magicodes.IE.Html** | **[![NuGet](https://buildstats.info/nuget/Magicodes.IE.Html)](https://www.nuget.org/packages/Magicodes.IE.Html)**   |
| **Magicodes.IE.Csv** | **[![NuGet](https://buildstats.info/nuget/Magicodes.IE.Csv)](https://www.nuget.org/packages/Magicodes.IE.Csv)**   |
| **Magicodes.IE.AspNetCore** | **[![NuGet](https://buildstats.info/nuget/Magicodes.IE.AspNetCore)](https://www.nuget.org/packages/Magicodes.IE.AspNetCore)**   |

### **Note**

- Excel import does not support ".xls" files, that is, Excel97-2003 is not supported. 
- For use in Docker, please refer to the section "Use in Docker" in the documentation. 
- Relevant functions have been compiled with unit tests. You can refer to unit tests during the use process. 

### **Tutorial**

1. <a href="docs/1.Basic tutorial of importing student data.md">Basic tutorial of importing student data</a>
2. <a href="docs/2.Basic tutorial of export Excel.md">Basic tutorial of export Excel</a>
3. <a href="docs/3.Basic tutorial of export Pdf receipts.md">Basic tutorial of export Pdf receipts</a>
4. <a href="docs/4.Use in Docker.md">Use in Docker</a>
5. <a href="docs/5.Dynamic Export.md">Dynamic Export</a>
6. <a href="docs/6.Import Multi-Sheet Tutorial.md">Import Multi-Sheet Tutorial</a>
7. <a href="docs/8. Import and export Excel as pictures.md">Import and export Excel as pictures</a>
8. <a href="docs/9.Excel template export-Export textbook order form .md">Excel template export-Export textbook order form</a>
9. <a href="docs/Excel Merge Row Cells Import.md">Excel Merge Row Cells Import</a>
12. <a href="docs/12.Exporting multiple formats in NETCore via request headers.md">Exporting multiple formats in NETCore via request headers</a>
13. <a href="docs/13.Performance Measurement.md">Performance Measurement</a>
14. <a href="docs/Excel Merge Row Cells Import.md">Excel Merge Row Cells Import</a>
15. <a href="docs/Excel template  export - dynamic export.md">Excel template  export - dynamic export</a>

**See below for other tutorials or unit tests**

**See below for update history.**

## Features

- **Need to be used in conjunction with related import and export DTO models, support import and export through DTO and related characteristics. Configure features to control related logic and display results without modifying the logic code;**
**![](./res/导入Dto.png "导入Dto")**
- **Support various filters to support scenarios such as multi-language, dynamic control column display, etc. For specific usage, see unit test:**
  - **Import column header filter (you can dynamically specify the imported column and imported value mapping relationship)**
  - **Export column header filter (can dynamically control the export column, support dynamic export (DataTable))**
  - **Import result filter (can modify annotation file)**
- **Export supports text custom filtering or processing;**
- **Import supports automatic skipping of blank lines in the middle;**
- **Import supports automatically generate import templates based on DTO, and automatically mark required items;**
![](./res/自动生成的导入模板.png "自动生成的导入模板")
- **Import supports data drop-down selection, currently only supports enumerated types;**
- **Imported data supports the processing of leading and trailing spaces and intermediate spaces, allowing specific columns to be set;**
- **Import supports automatic template checking, automatic data verification, unified exception handling, and unified error encapsulation, including exceptions, template errors and row data errors;**
![](./res/数据错误统一返回.png "数据错误")
- **Support import header position setting, the default is 1;**
- **Support import columns out of order, no need to correspond one to one in order;**
- **Support to import the specified column index, automatic recognition by default;**
- **Exporting Excel supports splitting of Sheets, only need to set the value of [MaxRowNumberOnASheet] of the characteristic [ExporterAttribute]. If it is 0, no splitting is required. See unit test for details;**
- **Support importing into Excel for error marking;**
![](./res/数据错误.png "数据错误标注")
![](./res/多个错误.png "多个错误")
- **Import supports cutoff column setting, if not set, blank cutoff will be encountered by default;**
- **Support exporting HTML, Word, Pdf, support custom export template;**
  -**Export HTML**
![](./res/导出html.png "导出HTML")
  -**Export Word**
![](./res/导出Word.png "导出Word")
  -**Export Pdf, support settings, see the update log for details**
![](./res/导出Pdf.png "导出Pdf")
  -**Export receipt**
![](./res/导出收据.png "导出收据.png")
- **Import supports repeated verification;**
![](./res/重复错误.png "重复错误.png")
- **Support single data template export, often used to export receipts, credentials and other businesses**
- **Support dynamic column export (based on DataTable), and the Sheet will be split automatically if it exceeds 100W. (Thanks to teacher Zhang Shanyou ([https://github.com/xin-lai/Magicodes.IE/pull/8](https://github.com/xin-lai/Magicodes.IE/pull/8) ))* *
- **Support dynamic/ExpandoObject dynamic column export**
```csharp
        [Fact(DisplayName = "DTO导出支持动态类型")]
        public async Task ExportAsByteArraySupportDynamicType_Test()
        {
            IExporter exporter = new ExcelExporter();

            var filePath = GetTestFilePath($"{nameof(ExportAsByteArraySupportDynamicType_Test)}.xlsx");

            DeleteFile(filePath);

            var source = GenFu.GenFu.ListOf<ExportTestDataWithAttrs>();
            string fields = "text,number,name";
            var shapedData = source.ShapeData(fields) as ICollection<ExpandoObject>;

            var result = await exporter.ExportAsByteArray<ExpandoObject>(shapedData);
            result.ShouldNotBeNull();
            result.Length.ShouldBeGreaterThan(0);
            File.WriteAllBytes(filePath, result);
            File.Exists(filePath).ShouldBeTrue();
        }
```
- **Support value mapping, support setting value mapping relationship through "ValueMappingAttribute" feature. It is used to generate data validation constraints for import templates and perform data conversion. **
```csharp
        /// <summary>
        ///     性别
        /// </summary>
        [ImporterHeader(Name = "性别")]
        [Required(ErrorMessage = "性别不能为空")]
        [ValueMapping(text: "男", 0)]
        [ValueMapping(text: "女", 1)]
        public Genders Gender { get; set; }
```

- **Support the generation of imported data verification items of enumeration and Bool type, and related data conversion**
	- **Enumeration will automatically obtain the description, display name, name and value of the enumeration by default to generate data items**

		```csharp
			/// <summary>
			/// 学生状态 正常、流失、休学、勤工俭学、顶岗实习、毕业、参军
			/// </summary>
			public enum StudentStatus
			{
				/// <summary>
				/// 正常
				/// </summary>
				[Display(Name = "正常")]
				Normal = 0,

				/// <summary>
				/// 流失
				/// </summary>
				[Description("流水")]
				PupilsAway = 1,

				/// <summary>
				/// 休学
				/// </summary>
				[Display(Name = "休学")]
				Suspension = 2,

				/// <summary>
				/// 勤工俭学
				/// </summary>
				[Display(Name = "勤工俭学")]
				WorkStudy = 3,

				/// <summary>
				/// 顶岗实习
				/// </summary>
				[Display(Name = "顶岗实习")]
				PostPractice = 4,

				/// <summary>
				/// 毕业
				/// </summary>
				[Display(Name = "毕业")]
				Graduation = 5,

				/// <summary>
				/// 参军
				/// </summary>
				[Display(Name = "参军")]
				JoinTheArmy = 6,
			}
		```

		![](./res/enum.png "枚举转数据映射序列")

	- **The bool type will generate "yes" and "no" data items by default**
	- **If custom value mapping has been set, no default options will be generated**

- **Support excel multi-sheet import**
  **![](./res/multipleSheet.png "枚举转数据映射序列")**

- **Support Excel template export, and support image rendering**
  **![](./res/ExcelTplExport.png "Excel模板导出")**

  The rendering syntax is as follows:

  ```
    {{Company}}  //Cell rendering
    {{Table>>BookInfos|RowNo}} //Table rendering start syntax
    {{Remark|>>Table}}//Table rendering end syntax
    {{Image::ImageUrl?Width=50&Height=120&Alt=404}} //Picture rendering
    {{Image::ImageUrl?w=50&h=120&Alt=404}} //Picture rendering
    {{Image::ImageUrl?Alt=404}} //Picture rendering
  ```

  Custom pipelines will be supported in the future.

- **Support Excel import template to generate annotation**
  ![](./res/ImportLabel.png "Excel导入标注")

- **Support Excel image import and export**
  - Picture import
    - Import as Base64
    - Import to temporary directory
    - Import to the specified directory
   - Picture export
    - Export file path as picture
    - Export network path as picture

- **Support multiple entities to export multiple Sheets**

- **Support using some features under the System.ComponentModel.DataAnnotations namespace to control import and export**
- - **Support the use of custom formatter in ASP.NET Core Web API to export content such as Excel, Pdf, Csv** 

- **Support export by column, sheet, and additional rows** 

```csharp
exporter.Append(list1).SeparateByColumn().Append(list2).ExportAppendData(filePath);
```

For details, see the above tutorial "Magicodes.IE Fancy Export"

- **Support cell export width setting**

```csharp
[ExporterHeader(Width = 100)]
public DateTime Time3 { get; set; }
```

- **Excel export supports HeaderRowIndex. Add the HeaderRowIndex attribute to the ExcelExporterAttribute export attribute class, so that it is convenient to specify the export from the first row when exporting. **

- **Excel generated import template supports built-in data verification**

The support for the built-in data validation can be turned on through the IsInterValidation attribute, and it should be noted that only MaxLengthAttribute, MinLengthAttribute, StringLengthAttribute, and RangeAttribute support the opening operation of the built-in data validation.

![](./res/dataval1.png "Excel验证")
![](./res/dataval2.png "Excel验证")

Support display operations for input prompts:
![](./res/dataval3.png "Excel验证")



### **Update history**

**[Update history](RELEASE.md)**



