```
def export_xls(request):
    response = HttpResponse(content_type='application/ms-excel')
    response['Content-Disposition'] = 'attachment; filename="example.xls"'
    wb = xlwt.Workbook(encoding='utf-8')
    ws = wb.add_sheet('Paymentmodewise Report')
	
    # Sheet header, first row
    row_num = 0

    font_style = xlwt.XFStyle()
    font_style.font.bold = True

    columns = ['columns_1', 'columns_2 'columns_3', 'columns_4']
    for col_num in range(len(columns)):
        ws.write(row_num, col_num, columns[col_num], font_style)

    # Sheet body, remaining rows
    font_style = xlwt.XFStyle()

    download_list = request.POST.getlist('id[]')

    if download_list:
        
        rows = Transactioninformation.objects.filter \
            (id__in=download_list).values_list('columns_1',
                                               'columns_2',
                                               'columns_3',
                                               'columns_4')
        request.session['download_list'] = download_list
        
		i = 1
        while (i < len(rows)):
            print(rows[i][i])
            i = i + 1
        for row in rows:
            row_num += 1
            ws.write(row_num, 0, row[0], font_style)
            ws.write(row_num, 1, row[1], font_style)
            ws.write(row_num, 2, row[2], font_style)
            ws.write(row_num, 3, row[3], font_style)
        row_num = row_num + 2
        ws.write_merge(0, 1, 0, 3, "Example",
                       xlwt.easyxf("font: bold on; align: vert centre, horiz center"))

        ws.write(row_num, 2, "Total", font_style)
        ws.write(row_num, 3, "BDT ", font_style)
		
        wb.save(response)
		
        return response
    else:
        download_list = request.session.get('download_list')
        rows = Transactioninformation.objects.filter \
            (id__in=download_list).values_list('columns_1',
                                               'columns_2',
                                               'columns_3',
                                               'columns_4')
        request.session['download_list'] = download_list
        
		i = 1
        while (i < len(rows)):
            print(rows[i][i])
            i = i + 1
        for row in rows:
            row_num += 1
            ws.write(row_num, 0, row[0], font_style)
            ws.write(row_num, 1, row[1], font_style)
            ws.write(row_num, 2, row[2], font_style)
            ws.write(row_num, 3, row[3], font_style)
        row_num = row_num + 2
        ws.write_merge(0, 1, 0, 3, "Example",
                       xlwt.easyxf("font: bold on; align: vert centre, horiz center"))

        ws.write(row_num, 2, "Total", font_style)
        ws.write(row_num, 3, "BDT ", font_style)
		
        wb.save(response)
		
        return response
```
