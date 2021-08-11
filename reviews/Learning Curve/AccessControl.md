# Access Control
## Created by: [Ben Beale](https://github.com/bbeale), [Marcel Jackish](https://github.com/marceljay)

## Summary
The contracts work permissionlessly after deployment.
There is no ownership or access control. 

## Scope
```
├── contracts
│   ├── KernelFactory.sol
│   └── LearningCurve.sol
```

## Files
### LearningCurve.sol
Add  the [`initializer`](https://docs.openzeppelin.com/contracts/4.x/api/proxy#Initializable) and onlyOwner ['onlyOwner'](https://docs.openzeppelin.com/contracts/4.x/api/access#Ownable) modifiers. 
