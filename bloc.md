# Шаблоны для BLoC
  
  
| Name                       | Expression                   | Default value                                       | Skip if defined |
|----------------------------|------------------------------|-----------------------------------------------------|-----------------|
| `NAME`                     |                              | `capitalize(camelCase(fileNameWithoutExtension()))` |                 |
| `fileNameWithoutExtension` | `fileNameWithoutExtension()` | `""`                                                | `x`             |

  
---
  
`blocFreezed`
```dart
import 'package:bloc/bloc.dart';
import 'package:freezed_annotation/freezed_annotation.dart';

part '$fileNameWithoutExtension$.freezed.dart';

@freezed
abstract class $NAME$Event with _$$$NAME$Event {
  const $NAME$Event._();

  const factory $NAME$Event.create() = Create$NAME$Event;

  const factory $NAME$Event.read() = Read$NAME$Event;

  const factory $NAME$Event.update() = Update$NAME$Event;

  const factory $NAME$Event.delete() = Delete$NAME$Event;
}

@freezed
abstract class $NAME$State with _$$$NAME$State {
  const $NAME$State._();
  
  const factory $NAME$State.initial() = Initial$NAME$State;
}

class $NAME$BLoC extends Bloc<$NAME$Event, $NAME$State> {
  $NAME$BLoC() : super(const Initial$NAME$State());

  @override
  Stream<$NAME$State> mapEventToState($NAME$Event event) =>
    event.when<Stream<$NAME$State>>(
      create: _create,
      read: _read,
      update: _update,
      delete: _delete,
    );
  
  Stream<$NAME$State> _create() async* {
    // ...    
  }

  Stream<$NAME$State> _read() async* {
    // ...
  }

  Stream<$NAME$State> _update() async* {
    // ...
  }

  Stream<$NAME$State> _delete() async* {
    // ...
  }
}
```

# Шаблоны для BLoC VS Code

```
{
	"blocFreezed": {
		"scope": "dart, flutter",
		"prefix": "blocFreezed",
		"body": [
			"import 'package:bloc/bloc.dart';",
			"import 'package:freezed_annotation/freezed_annotation.dart';",
			"",
			"part '${TM_FILENAME_BASE}.freezed.dart';",
			"",
			"@freezed ",
			"class ${NAME}Event with _$${NAME}Event {",
			"  const ${NAME}Event._();",
			"",
			"  const factory ${NAME}Event.request() = Request${NAME}Event;",
			"",
			"}",
			"",
			"@freezed",
			"class ${NAME}State with _$${NAME}State {",
			"  const ${NAME}State._();",
			"",
			"  const factory ${NAME}State.initial() = Initial${NAME}State;",
			"}",
			"",
			"class ${NAME}BLoC extends Bloc<${NAME}Event, ${NAME}State> {",
			"  ${NAME}BLoC() : super(const Initial${NAME}State());",
			"",
			"  @override",
			"  Stream<${NAME}State> mapEventToState(${NAME}Event event) =>",
			"    event.when<Stream<${NAME}State>>(",
			"      request: _request,",
			"  );",
			"",
			"  Stream<${NAME}State> _request() async* {",
			"    // ...",
			"  }",
			"",
			"}",
      ""
		]
	}
}
```

# Шаблоны для BLoC 8 VS Code

```
{
	"bloc8Freezed": {
		"scope": "dart, flutter",
		"prefix": "bloc8Freezed",
		"body": [
			"import 'package:bloc/bloc.dart';",
			"import 'package:freezed_annotation/freezed_annotation.dart';",
			"",
			"part '${TM_FILENAME_BASE}.freezed.dart';",
			"",
			"@freezed ",
			"class ${NAME}Event with _$${NAME}Event {",
			"  const ${NAME}Event._();",
			"",
			"  const factory ${NAME}Event.request() = _Request${NAME}Event;",
			"",
			"}",
			"",
			"@freezed",
			"class ${NAME}State with _$${NAME}State {",
			"  const ${NAME}State._();",
			"",
			"  const factory ${NAME}State.initial() = _Initial${NAME}State;",
			"}",
			"",
			"class ${NAME}BLoC extends Bloc<${NAME}Event, ${NAME}State> {",
			"  ${NAME}BLoC() : super(const ${NAME}State.initial()) {",
			"    on<${NAME}Event>(",
			"      (event, emitter) async {",
			"        await event.map<Future<void>>(",
			"          request: (event) => _request(event, emitter),",
			"        );",
			"      },",
			"    );",
			"  }",
			"",
			"  Future<void> _request(_Request${NAME}Event event,",
      "      Emitter<${NAME}State> emitter) async {}",
			"}",
      ""
		]
	}
}
