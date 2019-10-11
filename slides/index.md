- title : language-ext
- description : Introduction to lanaguage-ext
- author : Skylark
- theme : night
- transition : default

***

### language-ext

- Pyramid of doom
- Primitive Obsession
- Validation

***

### Pyramid of Doom

![Pyramid of Doom](images/pyramid-of-doom.jpg)


> **Atwood's Law**: any application that can be written in JavaScript, will eventually be written in JavaScript.

***

### Railway Oriented Programming

![ROP](images/rop.jpg)

***

### ROP in Code

    [lang=cs]
    var result =
        await ParseProfileIdOrValidationError(workflow.UserId)
        .BindAsync(uId => ValidateUserCanWriteToProfile(uId,
                            workflow.UserClaims)
        .Bind(_ => ValidateInputIsNotNull(workflow.InputModel))
        .Bind(_ => ValidateOnlyWhitelistedPropertiesAreSet(workflow.InputModel, uId,
                    workflow.UserClaims))
        .Bind(_ => ValidateUserDetailsInput(workflow.InputModel))
        .BindAsync(_ => CheckIfProfileExists(qs, uId, workflow))
        .BindAsync(_ => CheckUniqueFieldsForUpdate(qs, workflow.InputModel, uId,
                            workflow.UserClaims, workflow))
        .MapAsync(_ => MapModel(uId, workflow.ProfileFieldsToDelete))
        .MapAsync(CreateCommand));

    return result;

---

#### Workflow Method

    [lang=cs]
    public static Either<Error, Unit> ValidateUserCanWriteToProfile(UserId userId,
                                        UserClaims userClaims)
    {
        if (userClaims.IsAdmin == false
            && userClaims.IsUser(userId) == false
            && userClaims.ProfileRights.Write == false) return Errors.PermissionDenied;
        return unit;
    }

---

***

### The Reality of a Developer's Life 

**When I show my boss that I've fixed a bug:**
  
![When I show my boss that I've fixed a bug](http://www.topito.com/wp-content/uploads/2013/01/code-07.gif)
  
**When your regular expression returns what you expect:**
  
![When your regular expression returns what you expect](http://www.topito.com/wp-content/uploads/2013/01/code-03.gif)
  
*from [The Reality of a Developer's Life - in GIFs, Of Course](http://server.dzone.com/articles/reality-developers-life-gifs)*

