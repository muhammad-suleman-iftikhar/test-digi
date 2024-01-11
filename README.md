# test-digi

**My Thoughts**
Code is not up to standards, improvements are required to be made in the code. Queries are being done in loop 
convertJobIdsInObjs() method, repeated code base, no proper commenting. No request validators and no try catches.

Below are some points that must be addressed ::
1. We must have proper success and response returning methods, we can create a trait (Response trait).
2. Use of helping methods or utilities for any operations like date as there is alot of usage of carbon
3. Where required use nested Ifs rather than having if's like for BookingRepo store() method
4. Early Returns are required. if ($user->user_type != env('CUSTOMER_ROLE_ID')) { } just return
5. Functions return types are not defined
6. **Single Responsibility Principal should be obeyed**
   a. EMail sending function should be created seprately $this->sendEmail( $subject , 'emails.session-ended', $dataEmail); 
       changed on many places still few left 
7. Sending Notification or emails should be a part of a **queue or job**. for example sendSMSNotificationToTranslator() method
8. **Request Validator** classes are missing need to have them to validate every request.
9. **Commented cod**e needs to be removed. If you need that write a proper comment or TODO to differentiate, though it exists but not on all the locations.
10. Must use **composer defined packages or http request provided by laravel** rather than using curl.
11. Does not make sense to repeat your code to have the same data 
    $data = array();
       $data['created_at'] = date('Y-m-d H:i:s');
       $data['will_expire_at'] = TeHelper::willExpireAt($job['due'], $data['created_at']);
       $data['updated_at'] = date('Y-m-d H:i:s');
       $data['user_id'] = $userid;
       $data['job_id'] = $jobid;
       $data['cancel_at'] = Carbon::now();
and             $job['status'] = 'pending';
    $job['created_at'] = Carbon::now();
    $job['updated_at'] = Carbon::now();
    $job['will_expire_at'] = TeHelper::willExpireAt($job['due'], date('Y-m-d H:i:s'));
    $job['updated_at'] = date('Y-m-d H:i:s');
    $job['cust_16_hour_email'] = 0;
    $job['cust_48_hour_email'] = 0;
    $job['admin_comments'] = 'This booking is a reopening of booking #' . $jobid;
is almost same $data can be reused.
12. Methods that are not being called must be remove like bookingExpireNoAccepted(), userLoginFailed(), alerts()
13. Try Catches are missing in every single method.
14. PSR standards for variables, no of characters on a single line method definations are not being followed.