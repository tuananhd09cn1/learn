add_field.blade.php
<div class="bootbox-form">
  <div class="form-group">
      <label for="field_name">Field Name</label>
      <input type="text" class="bootbox-input form-control"  name="field_name" id="field_name" />
  </div>
  
  <div class="form-group">
     <label for="field_description">Field Description</label>
     <input type="text" class="bootbox-input form-control"  name="field_description" id="field_description" />
  </div>
  
  <div class="form-group">
    <label for="field_type">Select type</label>
     <select class="bootbox-input form-control"  name="field_type" id="field_type">
        <option>Option</option>
        <option>Checkbox</option>
        <option>Textarea</option>
        <option>Text</option>
      </select>
  </div>
  <div class="form-group">
    <label for="field_value">Value</label>
    <textarea name="field_value" class="bootbox-input form-control"  id="field_value"></textarea>
  </div>
  <div class="form-group">
    <label for="default_value">Default Value</label>
     <textarea name="default_value" class="bootbox-input form-control" id="default_value"></textarea>
  </div>
  <div class="form-group">
    <label for="place_holder_value">Placeholder Value</label>
     <textarea name="place_holder_value" class="bootbox-input form-control" id="place_holder_value"></textarea>
  </div>
</div>
-------------------------
add_step.blade.php
<div class="bootbox-form">
  <div class="form-group">
      <label for="field_name">Field Name</label>
      <input type="text" class="bootbox-input form-control"  name="field_name" id="field_name" />
  </div>
  
  <div class="form-group">
     <label for="field_description">Field Description</label>
     <input type="text" class="bootbox-input form-control"  name="field_description" id="field_description" />
  </div>
  
  <div class="form-group">
    <label for="field_type">Select type</label>
     <select class="bootbox-input form-control"  name="field_type" id="field_type">
        <option>Option</option>
        <option>Checkbox</option>
        <option>Textarea</option>
        <option>Text</option>
      </select>
  </div>
  <div class="form-group">
    <label for="field_value">Value</label>
    <textarea name="field_value" class="bootbox-input form-control"  id="field_value"></textarea>
  </div>
  <div class="form-group">
    <label for="default_value">Default Value</label>
     <textarea name="default_value" class="bootbox-input form-control" id="default_value"></textarea>
  </div>
  <div class="form-group">
    <label for="place_holder_value">Placeholder Value</label>
     <textarea name="place_holder_value" class="bootbox-input form-control" id="place_holder_value"></textarea>
  </div>
</div>
----
@extends('layouts.default')

<?php
    use App\Core\View\Form;
    use App\Setting\Model\Menu;

    $optionStates = Menu::toOptionState();
?>

@section('title')
    @if (! Form::getData('menus.id'))
        <!--{{ trans('setting::view.Config loan form') }}-->
    @else
        {{ Form::getData('menus.name') }}
    @endif
@endsection

@section('css')
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/select2/4.0.1/css/select2.min.css" />
    <style type="text/css">
        .modal.bootbox:not(.modal-default) .btn {
            background-color: #00a65a;
            border-color: #008d4c;
        }   
        .modal.bootbox:not(.modal-default) .btn:hover {
            color: #fff;
            background-color: #398439;
            border-color: #255625;
        }
        
    </style>
    
@endsection
@section('content')
    <div class="row menu-group">
        <form action="{{ route('setting::admin.setting.menu.group.save') }}" method="post" class="form-horizontal" id="form-edit-menus" autocomplete="off">
            {!! csrf_field() !!}
            <input type="hidden" name="id" value="{{ Form::getData('menus.id') }}" />
        </form>
            <div class="col-md-12">
                <div class="box box-primary">
                    <div class="box-header with-border">
                        <div class="pull-left">
						    <button class="btn btn-primary" onclick="FormBuilder.addStep()"><i class="fa fa-plus"></i> Add Step</a>
				    	</div>
    		            <div class="pull-right">   
    		                <button class="btn btn-primary" onclick="FormBuilder.addStep()"><i class="fa fa-save"></i> Save</a>
    		            </div>
                    </div>
                    <div class="box-body">
                        <table class="table table-bordered" id="step_table">
                                <thead>
                                    <tr>
                                        <td class="col-lg-1 col-xs-1"> Function</td>
                                        <td class="col-lg-2 col-xs-1"> Name</td>
                                        <td class="col-lg-1 col-xs-1"> Time</td>
                                        <td class="col-lg-8 col-xs-8"> Content</td>
                                        <td class="col-xs-1 col-md-1"> Order</td>
                                    </tr>
                                </thead>
                                <tbody>
                                    <!--<tr>-->
                                    <!--    <td class="text-center">-->
                                    <!--        <button class="btn btn-primary" onclick="FormBuilder.openAddFieldForm(this)"><i class="fa fa-plus"></i></button>-->
                                    <!--        <button class="btn btn-danger"><i class="fa fa-trash"></i></button>-->
                                    <!--    </td>-->
                                    <!--    <td><input type="text" class="form-control" value="Step 1" name="name"/></td>-->
                                    <!--    <td><input type="text" class="form-control" value="30s" name="time"/></td>-->
                                    <!--    <td>-->
                                    <!--        <table class="table table-bordered" id="form_field_1">-->
                                    <!--            <tbody>-->
                                    <!--                <tr>-->
                                    <!--                    <td class="col-lg-2 col-xs-2">Description</td>-->
                                    <!--                    <td class="col-lg-8 col-xs-8"><textarea name="description" class="form-control">Description</textarea></td>-->
                                    <!--                    <td><input type="text" class="form-control"/></td>-->
                                    <!--                    <td class="col-lg-2 col-xs-2 text-center">-->
                                    <!--                        <button class="btn btn-danger"><i class="fa fa-trash"></i></button>-->
                                    <!--                        <button class="btn btn-success"><i class="fa fa-edit"></i></button>-->
                                    <!--                    </td>-->
                                    <!--                </tr>-->
                                    <!--                <tr>-->
                                    <!--                    <td class="col-lg-2 col-xs-2">Test Text</td>-->
                                    <!--                    <td class="col-lg-8 col-xs-8">-->
                                    <!--                        <input type="text" class="form-control" name="order"/>-->
                                    <!--                    </td>-->
                                    <!--                    <td><input type="text" class="form-control" name="order"/></td>-->
                                    <!--                    <td class="col-lg-2 col-xs-2 text-center">-->
                                    <!--                        <button class="btn btn-danger"><i class="fa fa-trash"></i></button>-->
                                    <!--                        <button class="btn btn-success"><i class="fa fa-edit"></i></button>-->
                                    <!--                    </td>-->
                                    <!--                </tr>-->
                                    <!--                <tr>-->
                                    <!--                    <td class="col-lg-2 col-xs-2">Test Select Box</td>-->
                                    <!--                    <td class="col-lg-8 col-xs-8">-->
                                    <!--                        <select class="bootbox-input form-control"  name="field_type" id="field_type">-->
                                    <!--                            <option>Option</option>-->
                                    <!--                            <option>Checkbox</option>-->
                                    <!--                            <option>Textarea</option>-->
                                    <!--                            <option>Text</option>-->
                                    <!--                         </select>-->
                                    <!--                    </td>-->
                                    <!--                    <td><input type="text" class="form-control" name="order"/></td>-->
                                    <!--                    <td class="col-lg-2 col-xs-2 text-center">-->
                                    <!--                        <button class="btn btn-danger"><i class="fa fa-trash"></i></button>-->
                                    <!--                        <button class="btn btn-success"><i class="fa fa-edit"></i></button>-->
                                    <!--                    </td>-->
                                    <!--                </tr>-->
                                    <!--                <tr>-->
                                    <!--                    <td class="col-lg-2 col-xs-2">Test Checkbox Button</td>-->
                                    <!--                    <td class="col-lg-8 col-xs-8">-->
                                    <!--                        <div class="checkbox">-->
                                    <!--                            <label><input type="checkbox" value="">Option 1</label>-->
                                    <!--                        </div>-->
                                    <!--                        <div class="checkbox">-->
                                    <!--                            <label><input type="checkbox" value="">Option 2</label>-->
                                    <!--                        </div>-->
                                    <!--                        <div class="checkbox">-->
                                    <!--                            <label><input type="checkbox" value="">Option 3</label>-->
                                    <!--                        </div>-->
                                    <!--                    </td>-->
                                    <!--                    <td><input type="text" class="form-control" name="order"/></td>-->
                                    <!--                    <td class="col-lg-2 col-xs-2 text-center">-->
                                    <!--                        <button class="btn btn-danger"><i class="fa fa-trash"></i></button>-->
                                    <!--                        <button class="btn btn-success"><i class="fa fa-edit"></i></button>-->
                                    <!--                    </td>-->
                                    <!--                </tr>-->
                                    <!--                <tr>-->
                                    <!--                    <td class="col-lg-2 col-xs-2">Test Radio Button</td>-->
                                    <!--                    <td class="col-lg-8 col-xs-8">-->
                                    <!--                        <div class="radio">-->
                                    <!--                          <label><input type="radio" name="optradio">Option 1</label>-->
                                    <!--                        </div>-->
                                    <!--                        <div class="radio">-->
                                    <!--                          <label><input type="radio" name="optradio">Option 2</label>-->
                                    <!--                        </div>-->
                                    <!--                        <div class="radio disabled">-->
                                    <!--                          <label><input type="radio" name="optradio">Option 3</label>-->
                                    <!--                        </div>-->
                                    <!--                    </td>-->
                                    <!--                    <td><input type="text" class="form-control" name="order"/></td>-->
                                    <!--                    <td class="col-lg-2 col-xs-2 text-center">-->
                                    <!--                        <button class="btn btn-danger"><i class="fa fa-trash"></i></button>-->
                                    <!--                        <button class="btn btn-success"><i class="fa fa-edit"></i></button>-->
                                    <!--                    </td>-->
                                    <!--                </tr>-->
                                    <!--            </tbody>-->
                                    <!--        </table>-->
                                    <!--    </td>-->
                                    <!--    <td><input type="text" class="form-control"/></td>-->
                                    <!--</tr>-->
                                </tbody>
                            </table>
                    </div>
                    <div class="box-footer">

                    </div>
                    </div>
                </div>
            </div>
    </div>
    <?php
        // Remove flash session
        Form::forget();
    ?>
@endsection

@section('script')
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.15.0/jquery.validate.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/select2/4.0.3/js/select2.full.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootbox.js/4.4.0/bootbox.min.js"></script>
    <script>
        var dataExample = [
                { id : 1,
                  step_name: "Step 1",
                  step_time: "30s",
                  step_description:"Ds1",
                  order: 1,
                  fields : [
                        { 
                          field_id : 1,
                          field_name : "Field 1",
                          field_description :"Field Description",
                          type : "Option",
                          value: ["Test","Test 2","Test 3","Test 4"],
                          default_value: "Test",
                          place_holder_value :"Select test",
                          order:1
                        },
                        { 
                          field_id : 2,
                          field_description :"Field Description",
                          field_name :"Field 2",
                          type : "Text",
                          value:  "",
                          default_value: "Test",
                          place_holder_value :"Text  test",
                          order: 2
                        },
                        { 
                          field_id : 3,
                          field_description :"Field Description",
                          field_name :"Field ",
                          type : "Textarea",
                          value:  "",
                          default_value: "Test",
                          place_holder_value :"Text  test",
                          order: 2
                        },
                         { 
                          field_id : 4,
                          field_description :"Field Description",
                          field_name :"Field 4",
                          type : "Checkbox",
                          value:  ["Test","Test 2","Test 3","Test 4"],
                          default_value: ["Test","Test 2"],
                          place_holder_value :"Text  test",
                          order: 2
                        }
                      ]
                },
                { id : 2,
                  step_name: "Step 2",
                  step_time: "30s",
                  step_description:"Ds1",
                  order: 1,
                  fields : [
                        { 
                          field_id : 5,
                          field_name : "Field 5",
                          field_description :"Field Description",
                          type : "Option",
                          value: ["Test","Test 2","Test 3","Test 4"],
                          default_value: "Test",
                          place_holder_value :"Select test",
                          order:1
                        },
                        { 
                          field_id : 6,
                          field_description :"Field Description",
                          field_name :"Field 6",
                          type : "Text",
                          value:  "",
                          default_value: "Test",
                          place_holder_value :"Text  test",
                          order: 2
                        },
                        { 
                          field_id : 7,
                          field_description :"Field Description",
                          field_name :"Field 7",
                          type : "Textarea",
                          value:  "",
                          default_value: "Test",
                          place_holder_value :"Text  test",
                          order: 2
                        },
                         { 
                          field_id : 8,
                          field_description :"Field Description",
                          field_name :"Field 8",
                          type : "Checkbox",
                          value:  ["Test","Test 2","Test 3","Test 4"],
                          default_value: ["Test","Test 2"],
                          place_holder_value :"Text  test",
                          order: 2
                        }
                      ]
                }
            ]
        var FormBuilder = {
                
                initForm : function(data){
                    var html = "";
                    for (var i =0 ; i< data.length; i++){
                        html += FormBuilder.openStep(data[i]);
                        for (var j=0; j < data[i].fields.length; j++){
                            html+= FormBuilder.initCField(data[i].fields[j]);
                        }
                        html += FormBuilder.closeStep();
                    }
                    
                    $("#step_table > tbody:last-child").append(html);
                },
                addStepData : function(){
                    var step = { id :"", 
                             step_name: "Step example",
                             step_time: "30s",
                             step_description:"Step description",
                             order: 1,
                             fields : []
                            }
                    var id = dataExample[dataExample.length-1].id + 1;  
                    step.id = id;
                    dataExample.push(step);
                },
                openAddFieldForm : function(option){
                    
                    // $.ajax({
                    //     type: "GET",
                    //     url:   baseUrl+'admin/setting/loan_config/add_field',
                    //     dataType: "html",
                    //     success: function (msg) {
                              bootbox.dialog({
                                title: 'Add Field',
                                message: FormBuilder.openFormFieldHtml(),
                                buttons: {
                                    cancel: {
                                     label: "Cancel",
                                        className: 'btn-danger',
                                        callback: function(){
                                        }
                                    },
                                  
                                    ok: {
                                        label: "Save",
                                        className: 'btn-info',
                                        callback: function(){
                                            console.log(FormBuilder.getDataFormAddField());
                                            FormBuilder.createField(FormBuilder.getDataFormAddField(),option);
                                        }
                                    }
                                }
                            });
                    //     }
                    // });
                },
                getDataFormAddField : function(){
                    return {
                        place_holder_value: $("#place_holder_value").val(),
                        default_value: $("#default_value").val(),
                        field_value: $("#field_value").val(),
                        field_type: $('#field_type_value').val(),
                        field_description: $("#field_description").val(),
                        field_name: $("#field_name").val()
                    }
                },
                createField : function(data,option){
                    console.log(option);
                    var html = "";
                    switch (data.field_type){
                        case "Option" : 
                            html = FormBuilder.createSelectBoxField(data);
                            break;
                        case "Text"   :
                            html = FormBuilder.createTextField(data);
                            break;
                        case "Checkbox":
                            html = FormBuilder.createCheckBoxField(data);
                            break;
                        case "Textarea":
                            html = FormBuilder.createTextAreaField(data);
                            break;
                        default:
                            html = FormBuilder.createTextField(data);
                    }
                    $("#"+option+" tr:last").after(html);
                },
                initCField : function (data){
                     var html = "";
                    switch (data.type){
                        case "Option" : 
                            html = FormBuilder.createSelectBoxField(data);
                            break;
                        case "Text"   :
                            html = FormBuilder.createTextField(data);
                            break;
                        case "Checkbox":
                            html = FormBuilder.createCheckBoxField(data);
                            break;
                        case "Textarea":
                            html = FormBuilder.createTextAreaField(data);
                            break;
                        default:
                            html = FormBuilder.createTextField(data);
                    }
                    return html;
                },
                createTextField : function (data){
                    var html ='<tr><td class="col-lg-2 col-xs-2">'+data.field_name+'</td>';
                        html +='<td class="col-lg-8 col-xs-8"><input type="text"" class="form-control"/></td>';
                        html +='<td><input type="text" class="form-control"/></td>';
                        html +='<td class="col-lg-2 col-xs-2 text-center">';
                        html +='<button class="btn btn-danger" style="margin-left:5px;"><i class="fa fa-trash"></i></button>';
                        html +='<button class="btn btn-success"><i class="fa fa-edit"></i></button>';
                        html +='</td></tr>';
                    return html;
                },
                createSelectBoxField : function(data){
                   var html = '<tr>'+
                        '<td class="col-lg-2 col-xs-2">'+data.field_name+'</td>'+
                        '<td class="col-lg-8 col-xs-8">'+
                            '<select class="bootbox-input form-control"  name="field_type" id="field_type">'+
                                '<option>Option</option>'+
                                '<option>Checkbox</option>'+
                                '<option>Textarea</option>'+
                                '<option>Text</option>'+
                             '</select>'+
                        '</td>'+
                        '<td><input type="text" class="form-control" name="order"/></td>'+
                        '<td class="col-lg-2 col-xs-2 text-center">'+
                            '<button class="btn btn-danger"><i class="fa fa-trash"></i></button>'+
                            '<button class="btn btn-success"><i class="fa fa-edit"></i></button>'+
                        '</td>'+
                    '</tr>'
                    return html;
                },
                createCheckBoxField: function(data){
                     var html='<tr>'+
                        '<td class="col-lg-2 col-xs-2">'+data.field_name+'</td>'+
                        '<td class="col-lg-8 col-xs-8">'+
                            '<div class="checkbox">'+
                                '<label><input type="checkbox" value="">Option 1</label>'+
                            '</div>'+
                            '<div class="checkbox">'+
                                '<label><input type="checkbox" value="">Option 2</label>'+
                            '</div>'+
                            '<div class="checkbox">'+
                                '<label><input type="checkbox" value="">Option 3</label>'+
                            '</div>'+
                        '</td>'+
                        '<td><input type="text" class="form-control" name="order"/></td>'+
                        '<td class="col-lg-2 col-xs-2 text-center">'+
                            '<button class="btn btn-danger"><i class="fa fa-trash"></i></button>'+
                            '<button class="btn btn-success"><i class="fa fa-edit"></i></button>'+
                        '</td>'+
                    '</tr>';
                    return html;
                },
                createTextAreaField : function(data){
                    var html ='<tr><td class="col-lg-2 col-xs-2">'+data.field_name+'</td>';
                        html +='<td class="col-lg-8 col-xs-8"><textarea name="description" class="form-control">Description</textarea></td>';
                        html +='<td><input type="text" class="form-control"/></td>';
                        html +='<td class="col-lg-2 col-xs-2 text-center">';
                        html +='<button class="btn btn-danger" style="margin-left:5px;"><i class="fa fa-trash"></i></button>';
                        html +='<button class="btn btn-success"><i class="fa fa-edit"></i></button>';
                        html +='</td></tr>';
                    return html;
                },
                addStep: function(){
                    FormBuilder.addStepData();
                    
                    var tableField = 'table_fields_'+dataExample[dataExample.length-1].id+'';
                    var html= '<tr>'+
                            '<td class="text-center">'+
                                '<button class="btn btn-primary" onclick="FormBuilder.openAddFieldForm(\''+tableField+'\')"><i class="fa fa-plus"></i></button>'+
                                '<button class="btn btn-danger"><i class="fa fa-trash"></i></button>'+
                            '</td>'+
                            '<td><input type="text" class="form-control" value="Step 1" name="name"/></td>'+
                            '<td><input type="text" class="form-control" value="30s" name="time"/></td>'+
                            '<td><table id="'+tableField+'"><tbody><tr></tr><tbody></table></td>'+
                            '<td><input type="text" class="form-control"/></td>'+
                        '</tr>'
                      
                        $("#step_table > tbody:last-child").append(html);
                },
                openStep: function(data){
                    var tableField = 'table_fields_'+data.id+'';
                    var html= '<tr>'+
                            '<td class="text-center">'+
                                '<button class="btn btn-primary" onclick="FormBuilder.openAddFieldForm(\''+tableField+'\')"><i class="fa fa-plus"></i></button>'+
                                '<button class="btn btn-danger"><i class="fa fa-trash"></i></button>'+
                            '</td>'+
                            '<td><input type="text" class="form-control" value="Step 1" name="name"/></td>'+
                            '<td><input type="text" class="form-control" value="30s" name="time"/></td>'+
                            '<td><table id="'+tableField+'">';
                    return html;
                },
                closeStep: function(){
                        var html='</table></td>'+
                            '<td><input type="text" class="form-control"/></td>'+
                        '</tr>'
                        return html;
                },
                openFormFieldHtml : function(){
                    var html = "";
                    html='<input type="hidden"  name="field_type_value" id="field_type_value" />'+
                        '<div class="bootbox-form">'+
                            '<div class="form-group">'+
                            '<label for="field_name">Field Name</label>'+
                            '<input type="text" class="bootbox-input form-control"  name="field_name" id="field_name" />'+
                        '</div>'+
                      '<div class="form-group">'+
                         '<label for="field_description">Field Description</label>'+
                         '<input type="text" class="bootbox-input form-control"  name="field_description" id="field_description" />'+
                      '</div>'+
                      '<div class="form-group">'+
                        '<label for="field_type">Select type</label>'+
                         '<select class="bootbox-input form-control"  name="field_type" id="field_type" onchange="FormBuilder.selectType(this)">'+
                           '<option value="Text">Text</option>'+
                            '<option value="Option">Option</option>'+
                            '<option value="Checkbox">Checkbox</option>'+
                            '<option value="Textarea">Textarea</option>'+
                          '</select>'+
                      '</div>'+
                      '<div class="form-group">'+
                        '<label for="field_value">Value</label>'+
                        '<textarea name="field_value" class="bootbox-input form-control"  id="field_value"></textarea>'+
                      '</div>'+
                      '<div class="form-group">'+
                        '<label for="default_value">Default Value</label>'+
                         '<textarea name="default_value" class="bootbox-input form-control" id="default_value"></textarea>'+
                      '</div>'+
                      '<div class="form-group">'+
                        '<label for="place_holder_value">Placeholder Value</label>'+
                         '<textarea name="place_holder_value" class="bootbox-input form-control" id="place_holder_value"></textarea>'+
                      '</div>'+
                    '</div>';
                    return html;
                },
                selectType: function(option){
                    $('#field_type_value').val($(option).val());
                },
                loadView: function ($url, $id) {
                    $.ajax({
                        type: "POST",
                        url:   $url,
                        dataType: "html",
                        success: function (msg) {
                            $('#' + $id).html(msg);
                            $('#' + $id).removeClass();
                        }
                    });
                },
                loadUnAsync: function ($url, $id) {
                    $.ajax({
                        type: "POST",
                        url:  $url,
                        dataType: "html",
                        async: false,
                        success: function (msg) {
                            $('#' + $id).html(msg);
                            $('#' + $id).removeClass();
                        }
                    });
                }
            }
            
        $(function() {
           FormBuilder.initForm(dataExample);
        });
    </script>
   
@endsection
---
<?php

Route::group([
    'prefix' => 'admin',
    'as' => 'admin.',
    'middleware' => 'admin',
], function() {
    Route::group([
        'prefix' => 'setting',
        'as' => 'setting.'
    ], function() {
	    Route::group([
	        'prefix' => 'menu',
	        'as' => 'menu.'
	    ], function() {
	        Route::group([
		        'prefix' => 'group',
		        'as' => 'group.'
		    ], function() {
		        Route::get('/','MenuGroupController@index')->name('index');
		        Route::get('add','MenuGroupController@add')->name('add');
        		Route::get('view/{id}','MenuGroupController@view')->name('view')->where('id', '[0-9]+');
		        Route::post('save','MenuGroupController@save')->name('save');
		        Route::delete('delete','MenuGroupController@delete')->name('delete');
		    });
	        Route::group([
		        'prefix' => 'item',
		        'as' => 'item.'
		    ], function() {
		        Route::get('/','MenuItemController@index')->name('index');
		        Route::get('add','MenuItemController@add')->name('add');
        		Route::get('view/{id}','MenuItemController@view')->name('view')->where('id', '[0-9]+');
		        Route::post('save','MenuItemController@save')->name('save');
		        Route::delete('delete','MenuItemController@delete')->name('delete');
		    });
	    });

	    Route::group([
	        'prefix' => 'province',
	        'as' => 'province.'
	    ], function() {
	        Route::get('/','ProvinceController@index')->name('index');
	        Route::get('add','ProvinceController@add')->name('add');
    		Route::get('view/{id}','ProvinceController@view')->name('view')->where('id', '[0-9]+');
	        Route::post('save','ProvinceController@save')->name('save');
	        Route::delete('delete','ProvinceController@delete')->name('delete');
		});
		Route::group([
	        'prefix' => 'loan_config',
	        'as' => 'loan_config.'
	    ], function() {
	        Route::get('/','LoanFormConfigController@index')->name('index');
	        Route::get('/add_field','LoanFormConfigController@addField')->name('addField');
	    });
    });
});
---
<?php

namespace App\Setting\Http\Controllers;

use DB;
use Log;
use Lang;
use Exception;
use App\Core\View\Menu;
use App\Core\View\Form;
use App\Core\View\Breadcrumb;
use App\Core\Http\Controllers\Controller;
use App\Setting\Model\Menu as MenuModel;
use Illuminate\Support\Facades\Input;
use Illuminate\Support\Facades\Validator;

use App\Findbank\Model\Borrower as BorrowerModel;
use App\Findbank\Model\Step as StepModel;
use App\Findbank\Model\LoanDefine as LoanDefineModel;
use App\Findbank\Model\LoanPurpose as LoanPurposeModel;

class LoanFormConfigController extends Controller
{
    /**
     * Construct more
     */
    protected function _construct()
    {
        Breadcrumb::add('Home', route('member::admin.member.index'), '<i class="fa fa-dashboard"></i>');
        Breadcrumb::add('Setting');
        Breadcrumb::add('Loan form');
        Menu::setActive(null, null, 'Setting');
    }
    
    /**
     * Field Config
     */
    public function index()
    {
        //var_dump(LoanDefineModel::getAll());
        return view('setting::form.loan.config');
    }
    
    /**
     * List field
     */
    public function addField()
    {
        //var_dump(LoanDefineModel::getAll());
        return view('setting::form.loan.add_field');
    }
}
