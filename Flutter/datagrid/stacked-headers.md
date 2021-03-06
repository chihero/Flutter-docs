---
layout: post
title: Stacked Headers in Flutter DataGrid | DataTable | Syncfusion
description: Learn about how to add stacked header rows and customize row height of stacked header rows in Syncfusion Flutter DataGrid.
platform: flutter
control: SfDataGrid
documentation: ug
---

# Stacked headers in Flutter Datagrid

The datagrid provides support to display an additional unbound header rows known as [StackedHeaderRows](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/stackedHeaderRows.html) that are spanned across the DataGrid columns. You can group one or more columns under each stacked header.

Each [StackedHeaderRow](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/StackedHeaderRow-class.html) contains [cells](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/StackedHeaderRow/cells.html) that hold a list of [StackedHeaderCell](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/StackedHeaderCell-class.html) where each `StackedHeaderCell` contains a number of child columns. The [StackedHeaderCell.columnNames](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/StackedHeaderCell/columnNames.html) property returns the columns grouped under the stacked header row. The [GridColumn.mappingName](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/GridColumn/mappingName.html) is a unique name used for mapping specific child columns grouped under the same stacked header row. The [StackedHeaderCell.child](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/StackedHeaderCell/child.html) property is used to load any type of widget to the corresponding stacked header cell.

{% tabs %}
{% highlight Dart %} 

import 'package:syncfusion_flutter_core/theme.dart';
import 'package:syncfusion_flutter_datagrid/datagrid.dart';

@override
Widget build(BuildContext context) {
  return SfDataGridTheme(
    data: SfDataGridThemeData(
        headerStyle: DataGridHeaderCellStyle(
            backgroundColor: const Color(0xFFF1F1F1))),
    child: SfDataGrid(
      gridLinesVisibility: GridLinesVisibility.both,
      headerGridLinesVisibility: GridLinesVisibility.both,
      source: _productDataSource,
      columns: <GridColumn>[
        GridNumericColumn(mappingName: 'orderId', headerText: 'ID'),
        GridTextColumn(mappingName: 'customerName', headerText: 'Name'),
        GridNumericColumn(mappingName: 'productId', headerText: 'ID'),
        GridTextColumn(mappingName: 'product', headerText: 'Product'),
      ],
      stackedHeaderRows: <StackedHeaderRow>[
        StackedHeaderRow(cells: [
          StackedHeaderCell(
              columnNames: ['orderId', 'customerName'],
              child: Container(
                  color: const Color(0xFFF1F1F1),
                  child: Center(child: Text('Customer Details')))),
          StackedHeaderCell(
              columnNames: ['productId', 'product'],
              child: Container(
                  color: const Color(0xFFF1F1F1),
                  child: Center(child: Text('Product Details'))))
        ])
      ],
    ),
  );
}

{% endhighlight %}
{% endtabs %}

![flutter datagrid shows stacked headers](images/stacked-headers/flutter-stacked-headers.png)

## Multi stacked headers

You can provide multiple stacked headers to the datagrid by adding the multiple `StackedHeaderRow` to the `SfDataGrid.stackedHeaderRows` collection.

{% tabs %}
{% highlight Dart %} 

import 'package:syncfusion_flutter_core/theme.dart';
import 'package:syncfusion_flutter_datagrid/datagrid.dart';

@override
Widget build(BuildContext context) {
  return SfDataGridTheme(
    data: SfDataGridThemeData(
        headerStyle: DataGridHeaderCellStyle(
            backgroundColor: const Color(0xFFF1F1F1))),
    child: SfDataGrid(
      gridLinesVisibility: GridLinesVisibility.both,
      headerGridLinesVisibility: GridLinesVisibility.both,
      source: _productDataSource,
      columns: <GridColumn>[
        GridNumericColumn(mappingName: 'orderId', headerText: 'ID'),
        GridTextColumn(mappingName: 'customerName', headerText: 'Name'),
        GridNumericColumn(mappingName: 'productId', headerText: 'ID'),
        GridTextColumn(mappingName: 'product', headerText: 'Product'),
      ],
      stackedHeaderRows: <StackedHeaderRow>[
        StackedHeaderRow(cells: [
          StackedHeaderCell(
              columnNames: ['orderId', 'customerName', 'productId', 'product'],
              child: Container(
                  color: const Color(0xFFF1F1F1),
                  child: Center(child: Text('Order Shipment Details')))),
        ]),
        StackedHeaderRow(cells: [
          StackedHeaderCell(
              columnNames: ['orderId', 'customerName'],
              child: Container(
                  color: const Color(0xFFF1F1F1),
                  child: Center(child: Text('Customer Details')))),
          StackedHeaderCell(
              columnNames: ['productId', 'product'],
              child: Container(
                  color: const Color(0xFFF1F1F1),
                  child: Center(child: Text('Product Details'))))
        ])
      ],
    ),
  );
}

{% endhighlight %}
{% endtabs %}

![flutter datagrid shows multi stacked headers](images/stacked-headers/flutter-multi-stacked-headers.png)

## Changing row height of stacked headers

You can change the height of stacked header rows by using the [SfDataGrid.onQueryRowHeight](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/onQueryRowHeight.html) callback.

You can also change the row height of stacked header row and column header row by using [headerRowHeight](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/headerRowHeight.html) property.

{% tabs %}
{% highlight Dart %} 

import 'package:syncfusion_flutter_core/theme.dart';
import 'package:syncfusion_flutter_datagrid/datagrid.dart';

@override
Widget build(BuildContext context) {
  return SfDataGridTheme(
    data: SfDataGridThemeData(
        headerStyle: DataGridHeaderCellStyle(
            backgroundColor: const Color(0xFFF1F1F1))),
    child: SfDataGrid(
      gridLinesVisibility: GridLinesVisibility.both,
      headerGridLinesVisibility: GridLinesVisibility.both,
      source: _productDataSource,
      onQueryRowHeight: (RowHeightDetails details) {
        if (details.rowIndex == 0) {
          return 70.0;
        }
        return null;
      },
      columns: <GridColumn>[
        GridNumericColumn(mappingName: 'orderId', headerText: 'ID'),
        GridTextColumn(mappingName: 'customerName', headerText: 'Name'),
        GridNumericColumn(mappingName: 'productId', headerText: 'ID'),
        GridTextColumn(mappingName: 'product', headerText: 'Product'),
      ],
      stackedHeaderRows: <StackedHeaderRow>[
        StackedHeaderRow(cells: [
          StackedHeaderCell(
              columnNames: ['orderId', 'customerName'],
              child: Container(
                  color: const Color(0xFFF1F1F1),
                  child: Center(child: Text('Customer Details')))),
          StackedHeaderCell(
              columnNames: ['productId', 'product'],
              child: Container(
                  color: const Color(0xFFF1F1F1),
                  child: Center(child: Text('Product Details'))))
        ])
      ],
    ),
  );
}

{% endhighlight %}
{% endtabs %}

![flutter datagrid shows customization of stacked header row heights](images/stacked-headers/flutter-stacked-header-row-height.png)