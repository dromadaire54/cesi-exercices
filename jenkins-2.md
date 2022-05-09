# Exercice jenkins (Partie 2)
## Ajout de tests unitaires
Ajouter les dépendances nécessaires pour faire les tests
```xml
		<dependency>
  			<groupId>org.mockito</groupId>
  			<artifactId>mockito-core</artifactId>
		  	<scope>test</scope>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
```

Ajouter un fichier ```HelloController.java```
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

	private final GreetingService greetingService;

	public HelloController(GreetingService greetingService) {
		this.greetingService = greetingService;
	}

	@GetMapping("/")
	public String index() {
		return this.greetingService.greet();
	}

}
```

Ajouter un fichier qui contiendra service ```GreetingService```.
```java
import org.springframework.stereotype.Service;

@Service
public class GreetingService {
    public String greet() {
		return "Hello, World";
	}
}
```

Ajouter un fichier de test ```HelloControllerTest.java```  dans le répertoire ```test/java/com/sample.springboot```
```Java
package com.sample.springboot;

import static org.mockito.Mockito.when;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.result.MockMvcResultHandlers;
import org.springframework.test.web.servlet.result.MockMvcResultMatchers;

@WebMvcTest(HelloController.class)
public class HelloControllerTest {
    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private GreetingService greetingService;

    @Test
    public void getGreetWebSvc() throws Exception {
        when(greetingService.greet()).thenReturn("Hella cesi classroom");    
        this.mockMvc.perform(MockMvcRequestBuilders
            .get("/")
            .contentType(MediaType.TEXT_PLAIN))
            .andExpect(MockMvcResultMatchers.status().isOk())
            .andDo(MockMvcResultHandlers.print())
            .andExpect(MockMvcResultMatchers.content().string("Hello cesi classroom"));
    }
}

```
Maintenant vous pouvez committer et ensuite pousser les modifications. Vérifier dans Jenkins si le build a bien été lancé. Normalement le test ne fonctionne pas faite les modifications pour que le test passe.

