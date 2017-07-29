# WepApiCoreAndSwagger
Exemplo simples de wep api aspnet.core com documentação utilizando swagger.

#Configurações na classe de Startup


        public void ConfigureServices(IServiceCollection services) {          
            
            services.AddMvc();
            
            services.AddSwaggerGen(c => {
                c.SwaggerDoc("v1",
                    new Swashbuckle.AspNetCore.Swagger.Info {
                        Title = "WepApi AspNet.Core",
                        Version = "v1",
                        Description = "Exemplo simples de WepApi AspNet.Core com documentação utilizando swagger.",
                        TermsOfService = "None",
                        Contact =
                        new Swashbuckle.AspNetCore.Swagger.Contact { Name = "threenine.co.uk", Email = "support@threenine.co.uk", Url = "https://threenine.co.uk" }
                    });
            });
        }
        
        public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory) {
            loggerFactory.AddConsole(Configuration.GetSection("Logging"));

            loggerFactory.AddDebug();

            app.UseMvc();
            
            app.UseSwagger(c => {
                c.PreSerializeFilters.Add((swagger, httpReq) => swagger.Host = httpReq.Host.Value);
            });

            app.UseSwaggerUI(c => {
                c.SwaggerEndpoint("/swagger/v1/swagger.json", "WepApi AspNet.Core V1");
            });
        }
