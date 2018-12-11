# Summary

* [I、Preface](README.md)
  * [1、Spring Security Community](11.md)
    * [1.1. Getting Help](11/11-getting-help.md)
    * [1.2. Becoming Involved](11/12-becoming-involved.md)
    * [1.3. Source Code](11/13-source-code.md)
    * [1.4. Apache 2 License](11/14-apache-2-license.md)
    * [1.5. Social Media](11/15-social-media.md)
  * [2、What’s New in Spring Security 5.1](2whats-new-in-spring-security-51.md)
    * 2.1. Servlet
    * 2.2. WebFlux
    * 2.3. Integrations
  * [3、Getting Spring Security](3getting-spring-security.md)
    * [3.1. Release Numbering](3getting-spring-security/31-release-numbering.md)
    * [3.2. Usage with Maven](32-usage-with-maven.md)
      * [3.2.1. Spring Boot with Maven](32-usage-with-maven/321-spring-boot-with-maven.md)
      * [3.2.2. Maven Without Spring Boot](32-usage-with-maven/322-maven-without-spring-boot.md)
      * [3.2.3. Maven Repositories](32-usage-with-maven/323-maven-repositories.md)
    * [3.3. Gradle](3getting-spring-security/33-gradle.md)
      * 3.3.1. Spring Boot with Gradle
      * 3.3.2. Gradle Without Spring Boot
      * 3.3.3. Gradle Repositories
  * [4、Project Modules](4project-modules.md)
    * [4.1. Core - spring-security-core.jar](41-core-spring-security-corejar.md)
    * [4.2. Remoting - spring-security-remoting.jar](42-remoting-spring-security-remotingjar.md)
    * [4.3. Web - spring-security-web.jar](43-web-spring-security-webjar.md)
    * [4.4. Config - spring-security-config.jar](44-config-spring-security-configjar.md)
    * [4.5. LDAP - spring-security-ldap.jar](45-ldap-spring-security-ldapjar.md)
    * [4.6. OAuth 2.0 Core - spring-security-oauth2-core.jar](46-oauth-20-core-spring-security-oauth2-corejar.md)
    * [4.7. OAuth 2.0 Client - spring-security-oauth2-client.jar](47-oauth-20-client-spring-security-oauth2-clientjar.md)
    * [4.8. OAuth 2.0 JOSE - spring-security-oauth2-jose.jar](48-oauth-20-jose-spring-security-oauth2-josejar.md)
    * [4.9. ACL - spring-security-acl.jar](49-acl-spring-security-acljar.md)
    * [4.10. CAS - spring-security-cas.jar](410-cas-spring-security-casjar.md)
    * [4.11. OpenID - spring-security-openid.jar](411-openid-spring-security-openidjar.md)
    * [4.12. Test - spring-security-test.jar](412-test-spring-security-testjar.md)
  * [5、Sample Applications](5sample-applications.md)
    * [5.1. Tutorial Sample](51-tutorial-sample.md)
    * [5.2. Contacts](52-contacts.md)
    * [5.3. LDAP Sample](53-ldap-sample.md)
    * [5.4. OpenID Sample](54-openid-sample.md)
    * [5.5. CAS Sample](55-cas-sample.md)
    * [5.6. JAAS Sample](56-jaas-sample.md)
    * [5.7. Pre-Authentication Sample](57-pre-authentication-sample.md)
* [II、 Servlet Applications](ii-servlet-applications.md)
  * [6、Java Configuration](ii-servlet-applications/6java-configuration.md)
    * [6.1.Hello Web Security Java Configuration](ii-servlet-applications/6java-configuration/61hello-web-security-java-configuration.md)
      * [6.1.1. AbstractSecurityWebApplicationInitializer](ii-servlet-applications/6java-configuration/61hello-web-security-java-configuration/611-abstractsecuritywebapplicationinitializer.md)
      * [6.1.2. AbstractSecurityWebApplicationInitializer without Existing Spring](ii-servlet-applications/6java-configuration/61hello-web-security-java-configuration/612-abstractsecuritywebapplicationinitializer-without-existing-spring.md)
      * [6.1.3. AbstractSecurityWebApplicationInitializer with Spring MVC](ii-servlet-applications/6java-configuration/61hello-web-security-java-configuration/613-abstractsecuritywebapplicationinitializer-with-spring-mvc.md)
    * [6.2. HttpSecurity](ii-servlet-applications/6java-configuration/62-httpsecurity.md)
    * [6.3. Java Configuration and Form Login](ii-servlet-applications/6java-configuration/63-java-configuration-and-form-login.md)
    * [6.4. Authorize Requests](ii-servlet-applications/6java-configuration/64-authorize-requests.md)
    * [6.5. Handling Logouts](ii-servlet-applications/6java-configuration/65-handling-logouts.md)
      * 6.5.1. LogoutHandler
      * 6.5.2. LogoutSuccessHandler
      * 6.5.3. Further Logout-Related References
    * 6.6. OAuth 2.0 Client
      * 6.6.1. ClientRegistration
      * 6.6.2. ClientRegistrationRepository
      * 6.6.3. OAuth2AuthorizedClient
      * 6.6.4. OAuth2AuthorizedClientRepository / OAuth2AuthorizedClientService
      * 6.6.5. RegisteredOAuth2AuthorizedClient
      * 6.6.6. AuthorizationRequestRepository
      * 6.6.7. OAuth2AuthorizationRequestResolver
      * 6.6.8. OAuth2AccessTokenResponseClient
    * 6.7. OAuth 2.0 Login
      * 6.7.1. Spring Boot 2.x Sample
        * Initial setup
        * Setting the redirect URI
        * Configure application.yml
        * Boot up the application
      * 6.7.2. Spring Boot 2.x Property Mappings
      * 6.7.3. CommonOAuth2Provider
      * 6.7.4. Configuring Custom Provider Properties
      * 6.7.5. Overriding Spring Boot 2.x Auto-configuration
        * Register a ClientRegistrationRepository @Bean
        * Provide a WebSecurityConfigurerAdapter
        * Completely Override the Auto-configuration
      * 6.7.6. Java Configuration without Spring Boot 2.x
      * 6.7.7. Additional Resources
    * 6.8. OAuth 2.0 Resource Server
      * 6.8.1. Dependencies
      * 6.8.2. Minimal Configuration
        * Specifying the Authorization Server
        * Startup Expectations
        * Runtime Expectations
      * 6.8.3. Specifying the Authorization Server JWK Set Uri Directly
      * 6.8.4. Overriding or Replacing Boot Auto Configuration
        * Using jwkSetUri\(\)
        * Using decoder\(\)
        * Exposing a JwtDecoder @Bean
      * 6.8.5. Configuring Authorization
        * Extracting Authorities Manually
      * 6.8.6. Configuring Validation
        * Customizing Timestamp Validation
        * Configuring a Custom Validator
      * 6.8.7. Configuring Claim Set Mapping
        * Customizing the Conversion of a Single Claim
        * Adding a Claim
        * Removing a Claim
        * Renaming a Claim
      * 6.8.8. Configuring Timeouts
    * 6.9. Authentication
      * 6.9.1. In-Memory Authentication
      * 6.9.2. JDBC Authentication
      * 6.9.3. LDAP Authentication
      * 6.9.4. AuthenticationProvider
      * 6.9.5. UserDetailsService
    * 6.10. Multiple HttpSecurity
    * [6.11. Method Security](ii-servlet-applications/6java-configuration/611-method-security.md)
      * 6.11.1. EnableGlobalMethodSecurity
      * 6.11.2. GlobalMethodSecurityConfiguration
    * 6.12. Post Processing Configured Objects
    * 6.13. Custom DSLs

