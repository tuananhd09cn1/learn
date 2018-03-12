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
						    <a href="{{ route('member::admin.member.add') }}" class="btn btn-success"><i class="fa fa-plus"></i> Add Step</a>
				    	</div>
    		            <div class="pull-right">   
    		                
    		            </div>
                    </div>
                    <div class="box-body">
                        <table class="table table-bordered">
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
                                    <tr>
                                        <td class="text-center">
                                            <button class="btn btn-primary" onclick="FormBuilder.openAddFieldForm(this)"><i class="fa fa-plus"></i></button>
                                            <button class="btn btn-danger"><i class="fa fa-trash"></i></button>
                                        </td>
                                        <td><input type="text" class="form-control" value="Step 1" name="name"/></td>
                                        <td><input type="text" class="form-control" value="30s" name="time"/></td>
                                        <td>
                                            <table class="table table-bordered" id="form_field_1">
                                                <tbody>
                                                    <tr>
                                                        <td class="col-lg-2 col-xs-2">Description</td>
                                                        <td class="col-lg-8 col-xs-8"><textarea name="description" class="form-control">Description</textarea></td>
                                                        <td><input type="text" class="form-control"/></td>
                                                        <td class="col-lg-2 col-xs-2 text-center">
                                                            <button class="btn btn-danger"><i class="fa fa-trash"></i></button>
                                                            <button class="btn btn-success"><i class="fa fa-edit"></i></button>
                                                        </td>
                                                    </tr>
                                                    <tr>
                                                        <td class="col-lg-2 col-xs-2">Test Text</td>
                                                        <td class="col-lg-8 col-xs-8">
                                                            <input type="text" class="form-control" name="order"/>
                                                        </td>
                                                        <td><input type="text" class="form-control" name="order"/></td>
                                                        <td class="col-lg-2 col-xs-2 text-center">
                                                            <button class="btn btn-danger"><i class="fa fa-trash"></i></button>
                                                            <button class="btn btn-success"><i class="fa fa-edit"></i></button>
                                                        </td>
                                                    </tr>
                                                    <tr>
                                                        <td class="col-lg-2 col-xs-2">Test Select Box</td>
                                                        <td class="col-lg-8 col-xs-8">
                                                            <select class="bootbox-input form-control"  name="field_type" id="field_type">
                                                                <option>Option</option>
                                                                <option>Checkbox</option>
                                                                <option>Textarea</option>
                                                                <option>Text</option>
                                                             </select>
                                                        </td>
                                                        <td><input type="text" class="form-control" name="order"/></td>
                                                        <td class="col-lg-2 col-xs-2 text-center">
                                                            <button class="btn btn-danger"><i class="fa fa-trash"></i></button>
                                                            <button class="btn btn-success"><i class="fa fa-edit"></i></button>
                                                        </td>
                                                    </tr>
                                                    <tr>
                                                        <td class="col-lg-2 col-xs-2">Test Checkbox Button</td>
                                                        <td class="col-lg-8 col-xs-8">
                                                            <div class="checkbox">
                                                                <label><input type="checkbox" value="">Option 1</label>
                                                            </div>
                                                            <div class="checkbox">
                                                                <label><input type="checkbox" value="">Option 2</label>
                                                            </div>
                                                            <div class="checkbox">
                                                                <label><input type="checkbox" value="">Option 3</label>
                                                            </div>
                                                        </td>
                                                        <td><input type="text" class="form-control" name="order"/></td>
                                                        <td class="col-lg-2 col-xs-2 text-center">
                                                            <button class="btn btn-danger"><i class="fa fa-trash"></i></button>
                                                            <button class="btn btn-success"><i class="fa fa-edit"></i></button>
                                                        </td>
                                                    </tr>
                                                    <tr>
                                                        <td class="col-lg-2 col-xs-2">Test Radio Button</td>
                                                        <td class="col-lg-8 col-xs-8">
                                                            <div class="radio">
                                                              <label><input type="radio" name="optradio">Option 1</label>
                                                            </div>
                                                            <div class="radio">
                                                              <label><input type="radio" name="optradio">Option 2</label>
                                                            </div>
                                                            <div class="radio disabled">
                                                              <label><input type="radio" name="optradio">Option 3</label>
                                                            </div>
                                                        </td>
                                                        <td><input type="text" class="form-control" name="order"/></td>
                                                        <td class="col-lg-2 col-xs-2 text-center">
                                                            <button class="btn btn-danger"><i class="fa fa-trash"></i></button>
                                                            <button class="btn btn-success"><i class="fa fa-edit"></i></button>
                                                        </td>
                                                    </tr>
                                                </tbody>
                                            </table>
                                        </td>
                                        <td><input type="text" class="form-control"/></td>
                                    </tr>
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
        var FormBuilder = {
                openAddFieldForm : function(option){
                    $.ajax({
                        type: "GET",
                        url:   baseUrl+'admin/setting/loan_config/add_field',
                        dataType: "html",
                        success: function (msg) {
                              bootbox.dialog({
                                title: 'Add Field',
                                message: msg,
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
                                            FormBuilder.createField(FormBuilder.getDataFormAddField(),'form_field_1');
                                        }
                                    }
                                }
                            });
                        }
                    });
                },
                getDataFormAddField : function(){
                    return {
                        place_holder_value: $("#place_holder_value").val(),
                        default_value: $("#default_value").val(),
                        field_value: $("#field_value").val(),
                        field_type: $("#field_type").val(),
                        field_description: $("#field_description").val(),
                        field_name: $("#field_name").val()
                    }
                },
                createField : function(data,option){
                    var html ='<tr><td class="col-lg-2 col-xs-2">'+data.field_name+'</td>';
                        html +='<td class="col-lg-8 col-xs-8"><textarea name="description" class="form-control">Description</textarea></td>';
                        html +='<td><input type="text" class="form-control"/></td>';
                        html +='<td class="col-lg-2 col-xs-2 text-center">';
                        html +='<button class="btn btn-danger" style="margin-left:5px;"><i class="fa fa-trash"></i></button>';
                        html +='<button class="btn btn-success"><i class="fa fa-edit"></i></button>';
                        html +='</td></tr>';
                    $("#"+option+" tr:last").after(html);
                },
                addStep: function(){
                     
                                                    <tr>
                                                        <td class="col-lg-2 col-xs-2">Description</td>
                                                        <td class="col-lg-8 col-xs-8"><textarea name="description" class="form-control">Description</textarea></td>
                                                        <td><input type="text" class="form-control"/></td>
                                                        <td class="col-lg-2 col-xs-2 text-center">
                                                            <button class="btn btn-danger"><i class="fa fa-trash"></i></button>
                                                            <button class="btn btn-success"><i class="fa fa-edit"></i></button>
                                                        </td>
                                                    </tr>
                                                   
                                                </tbody>
                                            </table>
                                        </td>
                                        <td><input type="text" class="form-control"/></td>
                                    </tr>
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
