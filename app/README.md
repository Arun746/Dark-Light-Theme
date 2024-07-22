# app

A new Flutter project to implement dark/light theme.

## Getting Started

# (Implementing based on device dark/light mode)

Step 1 : Create ThemeDataStyle Class
 
                class ThemeDataStyle{
                    static ThemeData light =ThemeData(
                        usematerial3:bool,
                        brightness:Brightness.light,
                        colorScheme:colorScheme.light(
                            primary:   ,
                            background:,
                            secondary: ,
                        ),
                    );

                    static ThemeData dark =ThemeData(
                        usematerial3:bool,
                        brightness:Brightness.dark,
                        colorScheme:colorScheme.dark(
                            primary:   ,
                            background:,
                            secondary: ,
                        ),
                    );
                }

Step 2 : In main.dart add,
  theme: ThemeDataStyle.light, 
  darkTheme: ThemeDataStyle.dark,

Step 3 : implement style in widget
                 Container(
                       decoration: BoxDecoration(
                       color: Theme.of(context).colorScheme.primary,
                        borderRadius: BorderRadius.circular(20.0),
                       ),
                    height: 100.0,
                    child: const Center(
                    child: Text('Content'),
                   ),
                ),   

 --------------Now based on your system mode , color changes as defined in Theme data----------------------------

# (Implementing dynamic dark/light mode on app)
Step 1 : Create ThemeDataStyle Class
Step 2 : Create Provider to handle changes (with variable to store themedata;get and set themestyle ; changetheme function)
step 3 :In main.dart , wrap MyApp() with NotifierProvider as ,
                        void main() {
                                runApp(
                                   ChangeNotifierProvider(
                                   create: (context) => ThemeProvider(),
                                   child: const MyApp(),
                                  ),
                                );
                            }
Step 4 : Change theme value asin main.dart ,
                theme: Provider.of<ThemeProvider>(context).themeDataStyle,
Step 5 : Implementation of style in widget 

                           Widget build(BuildContext context) {
                                 final themeProvider = Provider.of<ThemeProvider>(context);
                                   return Scaffold(
                                    ----
                                    child: Center(
                                          child: Column(
                                             mainAxisAlignment: MainAxisAlignment.center,
                                              children: [
                                               Text(
                                               themeProvider.themeDataStyle == ThemeDataStyle.dark
                                               ? 'Dark Theme'
                                               : 'Light Theme',
                                               style: const TextStyle(fontSize: 25.0),
                                               ),
                                               const SizedBox(height: 10.0),
                                                Transform.scale(
                                                scale: 1.4,
                                                child: Switch(
                                                value: themeProvider.themeDataStyle == ThemeDataStyle.dark
                                                ? true
                                                : false,
                                                  onChanged: (isOn) {
                                                 themeProvider.changeTheme();
                                                 },
                                             ),
                                           ),
                                        ],
                                    ),
                                    ),
                                    ----
                                    );
                           } 

--------------Now based theme changes as defined in Theme data when transform bottom is toggled ----------------------------
        