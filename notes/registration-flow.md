1. 클라이언트가 localhost:8080 요청
2. Controller의 @GetMapping("") 어노테이션이 viewHomePage 메서드를 호출해 index.html 리턴
3. register 클릭 시 @{/register}로 controller의 /register 이동
4. ```@GetMapping("/register")
   public String showRegistrationForm(Model model) {
   model.addAttribute("user", new User());

   	return "signup_form";
   }
   ```
    user 객체를 생성해 model에 담아 view로 전송

5. form 태그의 @{/process_register} 경로로 user객체에 회원가입 정보를 담아 전송
6. ```@PostMapping("/process_register")
	public String processRegister(User user) {
		BCryptPasswordEncoder passwordEncoder = new BCryptPasswordEncoder();
		String encodedPassword = passwordEncoder.encode(user.getPassword());
		user.setPassword(encodedPassword);
		
		userRepo.save(user);
		
		return "register_success";
    }
    ```
   user 객체에 담긴 password를 암호화, userRepo.save로 user객체의 데이터를 JPA가 DB에 insert
7. register_success.html이 브라우저에 보여진다. (회원가입 완료)