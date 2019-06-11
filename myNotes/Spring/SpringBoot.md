# Spring Boot

1. @PathVariable 作用后：从URL中获取value，比如这样：

<pre>
@RequestMapping("/users/{username}")
    @ResponseBody
    public String userProfile(@PathVariable String username){
//        return String.format("user %s", username);
        return "user" + username; 
    }
<code> 