---
layout: post
title: a post with code
date: 2015-07-15 15:09:00
description: an example of a blog post with some code
tags: formatting code
categories: sample-posts
featured: true
---


# User Model Attributes
```
[Key]
public int UserId { get; set; }
public string UserName { get; set; }
public DateTime JoinedDate { get; set; }
public virtual IEnumerable<Order> Orders { get; set; }
```
# Order Model Attributes
```
[Key]
public int OrderId { get; set; }
public DateTime CreatedDate { get; set; }
public double Total { get; set; }
public int UserId { get; set; }
[ForeignKey("UserId")]
public User UserNavigation { get; set; }
```
# Create User Request Attributes
```
[Required(ErrorMessage = "Name of user is required")]
public string UserName { get; set; }
public DateTime JoinedDate { get; set; }
```
# Update User Request Attributes
```
[Required(ErrorMessage = "Name of user is required")]
public string UserName { get; set; }
```
# Get User Response Attributes
```
public string UserName { get; set; }
public DateTime JoinedDate { get; set; }
```

# IUserService Methods
```
Task<GetUserResponse> CreateUser(CreateUserRequest request);
Task<List<GetUserResponse>> GetUsers();
Task<GetUserResponse> UpdateUser(int id, UpdateUserRequest request);
Task<bool> DeleteUser(int id);
Task<GetUserResponse> GetUserById(int id);
```
# UserService Methods
```
    private readonly ApplicationDbContext _context;
    private IMapper _mapper;


    public UserService(ApplicationDbContext context, IMapper mapper)
    {
        _mapper = mapper;
        _context = context;
    }
    public async Task<GetUserResponse> CreateUser(CreateUserRequest request)
    {
        User user = _mapper.Map<User>(request);
        _context.Users.Add(user);
        await _context.SaveChangesAsync();
        return _mapper.Map<GetUserResponse>(user);
    }

    public async Task<bool> DeleteUser(int id)
    {
        var user = await _context.Users.FirstOrDefaultAsync(u => u.UserId == id);
        if (user == null)
        {
            return false;
        }
        _context.Users.Remove(user);
        await _context.SaveChangesAsync();
        return true;
    }

    public async Task<GetUserResponse> GetUserById(int id)
    {
        var user = await _context.Users.FirstOrDefaultAsync(u => u.UserId == id);
        return _mapper.Map<GetUserResponse>(user);

    }

    public async Task<List<GetUserResponse>> GetUsers()
    {
        var users = await _context.Users.ToListAsync();
        return _mapper.Map<List<GetUserResponse>>(users);
    }

    public async Task<GetUserResponse> UpdateUser(int id, UpdateUserRequest request)
    {
        var user = await _context.Users.FirstOrDefaultAsync(u => u.UserId == id);
        if (user == null)
        {
            return null;
        }
        _mapper.Map(request, user);
        await _context.SaveChangesAsync();
        return _mapper.Map<GetUserResponse>(user);
    }
```
# MapperConfig.cs
```
  public static MapperConfiguration RegisterMaps()
    {
        var mapperConfig = new MapperConfiguration(config =>
        {
            config.CreateMap<CreateUserRequest, User>().ReverseMap();
            config.CreateMap<UpdateUserRequest, User>().ReverseMap();
            config.CreateMap<GetUserResponse, User>().ReverseMap();
        });
        return mapperConfig;
    }
```

# Config mapper in program.cs
```
IMapper mapper = MapperConfig.RegisterMaps().CreateMapper();
builder.Services.AddSingleton(mapper);
builder.Services.AddAutoMapper(AppDomain.CurrentDomain.GetAssemblies());
```
