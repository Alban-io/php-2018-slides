```php
<?php declare(strict_types=1);

namespace MyApp\Route;

class UserRoute extends AbstractRoute implements UserProviderInterface, RouteInterface
{
    use RouteTrait;

    /** PHP RFC: Typed Properties 2.0 PHP 7.4 **/
    private LoggerInterface $logger;
    
    /** @var UserRepository */
    private $userRepository;

    /** @var Item[] */
    private $cache;

    public function __construct(
        LoggerInterface $logger,
        UserRepository $userRepository,
    ) {
        $this->logger = $logger;
        $this->userRepository = $userRepository;
    }

    public function getResources(
        string $userId,
        string ...$tags,
    ): ResponseInterface {

        return new ResponseData([
            'result' => $this->userRepository->getResources($userId, $tags),
            'availableAt' => $this->getAvailableAt() ?? time(),
        ]);
    }
}
```