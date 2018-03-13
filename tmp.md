https://github.com/careydevelopment/AllSpringBootDemos
https://github.com/careydevelopment/YouTubeAPIDemo.git
https://github.com/Litarvan/vget
http://www.littlebigextra.com/spring-boot-oauth2-tutorial-for-authorizing-through-facebook-google-linkedin-and-twitter/
http://www.littlebigextra.com/part-2-authorising-user-using-spring-social-google-facebook-linkedin-spring-security/
http://lorenzo-dee.blogspot.com/2016/08/spring-security-oauth2-with-google.html
https://github.com/lorenzodee/spring-security-oauth2-google
https://gigsterous.github.io/engineering/2017/03/01/spring-boot-4.html
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateTableBorrower extends Migration
{
    private $table = 'borrower';
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        if (Schema::hasTable($this->table)) {
            return;
        }
        Schema::create($this->table, function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->string('name', 200);
            $table->text('id_cmd', 500);
            $table->text('dob',500);
            $table->string('phone_number',200);
            $table->string('email',200);
            $table->integer('loan_info_id')->unsigned();
            $table->foreign('loan_info_id')->references('id')->on('loan_info');
            $table->dateTime('created_at');
            $table->dateTime('updated_at')->nullable();
            $table->dateTime('deleted_at')->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        //
    }
}

<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateTableLoanDefine extends Migration
{
    private $table = 'loan_define';
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        if (Schema::hasTable($this->table)) {
            return;
        }
        Schema::create($this->table, function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->string('field_name', 200);
            $table->text('field_value', 500);
            $table->text('default_value',500);
            $table->string('type',200);
            $table->integer('step_id')->unsigned();
            $table->foreign('step_id')->references('id')->on('step');
            $table->dateTime('created_at');
            $table->dateTime('updated_at')->nullable();
            $table->dateTime('deleted_at')->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
    }
}
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateTableLoanInfo extends Migration
{
    private $table = 'loan_info';
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        if (Schema::hasTable($this->table)) {
            return;
        }
        Schema::create($this->table, function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->string('email', 100);
            $table->string('loan_type', 100);
            $table->text('loan_money')->nullable();
            $table->tinyInteger('number_people_len')->default(1);
            $table->binary('data');
            $table->dateTime('updated_at')->nullable();
            $table->dateTime('deleted_at')->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::drop($this->table);
    }
}
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateTableStep extends Migration
{
    private $table = 'step';
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        if (Schema::hasTable($this->table)) {
            return;
        }
        Schema::create($this->table, function (Blueprint $table) {
            $table->increments('id');
            $table->string('name', 100);
            $table->text('description')->nullable();
            $table->tinyInteger('sort_order')->default(0);
            $table->dateTime('created_at');
            $table->dateTime('updated_at')->nullable();
            $table->dateTime('deleted_at')->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::drop($this->table);
    }
}
