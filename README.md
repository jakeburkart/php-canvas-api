# php-canvas-api
PHP library for talking to Instructure's Canvas via its API.

## Composer installation

`composer require longhornopen/canvas-api`

## Usage examples

        use LonghornOpen\CanvasApi\CanvasApiClient;
        
        $api_host = 'myschool.instructure.com';
        $access_key = '1234567890abcdef....';
        $api = new CanvasApiClient($api_host, $access_key);
        
        // Some API calls return a single object, which will be given as a stdClass.
        $me = $api->get('/users/self');
        echo($me->name);
        
        // Some API calls return lists, which will be given as PHP7 Iterators.
        // If there are multiple pages of results, the iterator will automatically fetch them.
        $my_courses = $api->get('/courses?per_page=100');
        foreach ($my_courses as $my_course) {
            echo($my_course->name);
        }

        // Some API calls (e.g. Enrollment Terms) return lists which are wrapped in a wrapper element, which you can provide:
        $terms = $api->get('/accounts/1/terms', 'enrollment_terms');

## Version history
* 1.0 - public release
