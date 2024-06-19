
# Link Harvester
Link Harvester is a simple app that collects links from users. Any user can submit links that are validated and stored by the application. Users can see the submitted (links/domains) and search, and sort those data. The results are displayed in a paginated table.




## Step-01: Setup Laravel Project

#### 01. Create a new laravel project

```bash
composer create-project --prefer-dist laravel/laravel src
```
#### 02. Navigate to the project directory
```bash
cd src
```



## Step-02: Add URLs Page

#### 01. Front-End Design with Alpine.js by cdn

```bash
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>

```
### ***Add Urls Page Screenshot 
![App Screenshot](https://ronyahmed.xyz/upload/service/page-01.png)



## Step-03: URL Validation and Processing

#### 01. Implement FormRequest validation to validate the submitted URLs.

```bash
php artisan make:request UrlRequest

```
#### 02. Create a Laravel Job to process the URLs and store them in the database
```bash
php artisan make:Job ProcessUrls
```
#### 03. Finally Process the job
```bash
php artisan queue:work
```


## Step-04 Create the Database Tables

### 1. Define migrations for two tables: domains and urls.

### 2. In the domains table, store the unique base domain names.

### 3. In the urls table, store the URLs along with a foreign key linking to the domains table.

```bash
  public function up() {
    Schema::create('domains', function (Blueprint $table) {
        $table->id();
        $table->string('name')->unique();
        $table->timestamps();
    });
}
```

```bash
public function up() {
    Schema::create('urls', function (Blueprint $table) {
        $table->id();
        $table->string('url')->unique();
        $table->foreignId('domain_id')->constrained('domains');
        $table->timestamps();
    });
}
```


## Step-05 Show URLs Page with search, sort and pagination

### ***Show Urls Page Screenshot 

![App Screenshot](https://ronyahmed.xyz/upload/service/page-02.png)




```
## How to Install and Run the Project

```bash 
1. git clone https://github.com/skrony013/link_harverster_without_dockerization.git

2. cp .env.example .env

3. composer update --no-scripts

4. php artisan serve and visit http://127.0.0.1:8000/
```