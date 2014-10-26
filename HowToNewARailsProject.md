#How to new a rails project

1. ```mkdir rails_project```
2. ```cd rails_project```
3. ```rails new job_board -T```
4. 如果有改過Gemfile, 都要```bundle install```
5. ```rail s```啟動rails server
    * 啟動後可以到<http://localhost:3000/rails/info>查看routes資訊   
    
6. 編輯route.rb
	i. REST類型懶人route-> ```resoueces :jobs```
	i. 普通route-> ```rails g controller pages```
	i. GET route-> ```get 'welcome/index'```
	i. 終端機輸入```rails generate controller job```   
	產生：   
		> controllers/jobs_controller.erb   
		views/jobs   
		helpers/jobs_helper.erb   
		assets/javascripts/jobs.js.coffee   
		assets/stylesheets/jobs.css.scss
		
		1. controller加上  
			```
				def index
				end
			```
		2. view新增index.html.erb
		3. 就能到<http://localhost:3000/jobs>看首頁了
7. 新增資料庫
	i. 終端機輸入```rails g model job```   
	會新增
		>db/migrate/時間戳記_create_jobs.rb   
		models/job.rb
	i. 編輯 時間戳記_create_jobs.rb   
		1. 在```create_table :jobs do |t|```下輸入你想增加的欄位   
		例如```t.text :title```   
		2. 儲存後終端機輸入```rake db:migrate```讓要新增的欄位寫進資料庫
	i. 也可以```rails g model group title:string description:string```
	再```rake db:migrate```
8. 要怎麼new一個job?   

		#new.html.erb
			<h1>Add a job</h1>
			<%= form_for @job do |f| %>
  			<div>
    			<%= f.label :title %>
    			<%= f.text_field :title %>
  			</div>
  			<div>
   		 		<%= f.label :description %>
   		 		<%= f.text_field :description %>
 			</div>
 		 	<div>
 		   		<%= f.submit %>
 		 	</div>
			<% end %>
		
		#jobs.controller.rb
			def new
   				@job = Job.new
 			end
 			
 			def create
    			Job.create(job_params)
    			redirect_to jobs_path
  			end

  			private
  			def job_params
    			params.require(:job).permit(:title, :description)
  			end
  	如果想查詢資料庫裡面有幾的Job   
  	可以在終端機輸入```rails c```(Rails console模式),接下來打```Job.count```系統會算給你   
  	要離開```rails c```模式,輸入```exit```
9. 顯示所有jobs    
	controller
	
		@jobs = Job.all   
		
	view
	
		<% @jobs.each do |job| %>
  			<h3><%= job.title %></h3>
  			<p><%= job.description %></p>
		<% end %>
10. 我的new跟edit頁面差不多,想要DRY,怎麼辦?   
	製作partial   
	
		#app/views/jobs/_form.html.erb
		<%= form_for @job do |f| %>
  			<div>
    			<%= f.label :title %>
    			<%= f.text_field :title %>
  			</div>
  			<div>
    			<%= f.label :description %>
    			<%= f.text_area :description, size: '60x6' %>
  			</div>
  			<div>
    			<%= f.submit %>
  			</div>
			<% end %>
			
	現在可以在new及edit裡面加上```<%= render "form" %>```引用form這個partial
	
---
非RESTful的route
新增controller: ```rails g controller pages```      

controller輸入   

	def welcome   
	end

view新增welcome.html.erb   

route輸入```root :to => ""pages#welcome""```   

_注意_ controller、view、route都必須同樣命名welcome才能成功印出內容