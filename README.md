# RestAPI-in-Oracle-APEX

# Direct JSON request body
declare
l_var clob;
begin
apex_web_service.g_request_headers (1).name := 'Content-Type';
apex_web_service.g_request_headers(1).value := 'application/json';

l_var := apex_web_service.make_rest_request(
p_url => 'https://apex.oracle.com/pls/apex/ccs2022/rest-v1/employees/',
p_http_method => 'POST',
p_body =>'
        {
          "DEPTNO": 50,
          "DNAME": "BANGLADESH",
          "LOC": 50
        }
');
end;


# Single or Multi parameters passin  name/value pairs.
--Make parametters is oracle apex
DECLARE
    l_clob 	CLOB;
BEGIN
    apex_web_service.g_request_headers (1).name := 'Content-Type';
    apex_web_service.g_request_headers(1).value := 'application/x-www-form-urlencoded';
    
    l_clob := apex_web_service.make_rest_request(
        p_url => 'https://apex.oracle.com/pls/apex/ccs2022/rest-v1/employees/',
        p_http_method => 'POST',
        p_parm_name => apex_string.string_to_table('DEPTNO:DNAME:LOC'),
        p_parm_value => apex_string.string_to_table('60:TEST:60')
        );
        htp.p(l_clob);
END;
